---
layout: post
category: 🤔
---

### **Situation**

테스트 환경이 dev, staing 테스트 점유로 환경이 점점 늘어나게 되었다.
SRE 인력이 줄다보니,,, 테라폼이 관리가 안되었고, 환경 관리가 ECS쪽 초기 배포할때 만 작업되어 이후 관리나, 다른 리소스들은 수동으로 만들어야 하는 상태였다.

내가 관리하는 서버는 환경을 구축 할 때 마다 S3 버킷만 5개 이상 생성해야했고.. 
환경이 구축될 때마다 환경변수, S3이름 등이 통일되지않고, 
만드는 사람들 마다 네이밍 방식도 달라 관리가 절실히 필요하다 싶어 직접 구축해야겠다 싶었다.

### **Action**

일단 새로 생성하는 admin front 환경을 Terraform 을 통해 작업을 해보기로 하였다. 

### **Result**

**설치**

```jsx
brew install terraform
```

### 목표

s3 버킷을 생성해보자. 

**terraform.tf**

terraform 관련 설정을 위해 사용하는 파일로 보인다. 튜토리얼을 보니  `terraform.tf` 를 만들어 관리해 주는 것 같아 안에 넣어두었다.

*required_providers* : 사용할 공급자를 구성. aws, docker 등등

```jsx
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0.2"
    }
  }
  required_version = "~> 1.7"
}
```

**main.tf**

공급자 및 메인 소스를 관리하는 것 같은데, 

일단은 [s3.tf](http://s3.tf) 에 다 넣어두고, 해당 파일에는 공급자만 넣어두었다. 

provider

사용하고싶은 제품을 지정한다. aws, google 등 다양하게 존재한다. 

```jsx
provider "aws" {
  profile = "new_staging"
  region = var.region
  access_key = var.AWS_ACCESS_KEY_ID
  secret_key = var.AWS_SECRET_ACCESS_KEY
}
```

**variables.tf**

환경변수를 정의하는 테라폼이다. S3에 사용하는 변수들을 넣어주었다.

```python
variable "bucket_name" { type = string }
variable "profile" { type = string }
variable "region" { type = string }
variable "object_ownership" { type = string }
variable "block_public_acls" { type = bool }
...
```

**{stage}.tfvars**

각각 환경별로 variable 파일을 만들어주었다. 아래의 형식대로 값이 넣어진다.

```python
profile = "..."
bucket_name = "..."
region = "us-west-2"
...
```

**s3.tf**

s3 관련 설정이다 버킷 이름 외에, `ownership`, `access` , `acl` 등 다양한 설정을 진행할 수 있다.

```python
resource "aws_s3_bucket" "naming" {
  bucket = var.bucket_name
}

resource "aws_s3_bucket_ownership_controls" "naming" {
  bucket = aws_s3_bucket.naming.id
  rule {
    object_ownership = var.object_ownership
  }
}

resource "aws_s3_bucket_public_access_block" "naming" {
  bucket = aws_s3_bucket.naming.id
  block_public_acls       = var.block_public_acls
  block_public_policy     = var.block_public_policy
  ignore_public_acls      = var.ignore_public_acls
  restrict_public_buckets = var.restrict_public_buckets
}

resource "aws_s3_bucket_acl" "naming" {
  depends_on = [
    aws_s3_bucket_ownership_controls.naming,
    aws_s3_bucket_public_access_block.naming,
  ]

  bucket = aws_s3_bucket.naming.id
  acl = var.aws_s3_bucket_acl
}
```

##### parameter store
parameter store 의 경우에는, each key를 사용해 따로 관리해주면 좋을 것 같아 작업했다.
이 변수는 따로 파일을 만들어 import 하는게 좋을 것 같다 생각했지만 당장 찾았을 때 나오는게 없었고
프론트 환경은 s3, cf, ssm 이 세가지의 값과 나머지는 azure-pipeline CD 환경에서 적용했어야 했기 때문에 
이정도면 무난할 것 같아 이렇게 작업을 진행하였다.

```python

# staging1.tfvars
env = {
    "NEXT_PUBLIC_API_URL" = {
        value="https://abc.com"
    }
}

# variables.tf
resource "aws_ssm_parameter" "cms-admin-params" {
  for_each = var.env
  name        = "/services/cms-front/${var.stage}/${each.key}"
  value       = each.value.value
  type        = "SecureString"

  tags = {
    environment = var.stage
  }
}
```

배포

```bash
terraform init
terraform plan -var-file "name.tfvars"
terraform apply -var-file "name.tfvars"
```

로 배포하면 잘 동작한다. 이렇게 CF, SSM까지 작업해서 완료!