
### 1. Creating an AWS EC2 Instance

```
provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe01e" # Replace with a valid AMI ID
  instance_type = "t2.micro"

  tags = {
    Name = "ExampleInstance"
  }
} 

```

This snippet creates a simple EC2 instance in AWS. Make sure to replace the AMI ID with one that is available in your chosen region.



### 2. Setting Up an S3 Bucket

```
provider "aws" {
  region = "us-west-2"
}

resource "aws_s3_bucket" "example" {
  bucket = "my-unique-bucket-name"
  acl    = "private"

  tags = {
    Name        = "ExampleBucket"
    Environment = "Dev"
  }
} 
```

This code creates an S3 bucket with a unique name and sets its access control list (ACL) to private. Remember to choose a globally unique bucket name.


### 3. Creating a VPC with Subnets

```
provider "aws" {
  region = "us-west-2"
}

resource "aws_vpc" "example" {
  cidr_block = "10.0.0.0/16"

  tags = {
    Name = "ExampleVPC"
  }
}


resource "aws_subnet" "example_subnet" {
  vpc_id            = aws_vpc.example.id
  cidr_block        = "10.0.1.0/24"
  availability_zone = "us-west-2a"

  tags = {
    Name = "ExampleSubnet"
  }
} 

```
This snippet sets up a Virtual Private Cloud (VPC) along with a subnet. It defines the CIDR block for the VPC and the subnet, ensuring proper network segmentation.



### 4. Deploying an RDS Instance

```
provider "aws" {
  region = "us-west-2"
}

resource "aws_db_instance" "example" {
  allocated_storage    = 20
  engine             = "mysql"
  engine_version     = "8.0"
  instance_class     = "db.t2.micro"
  name               = "exampledb"
  username           = "admin"
  password           = "password123" # Use a more secure method for production
  skip_final_snapshot = true

  tags = {
    Name = "ExampleRDS"
  }
} 

```
This code snippet creates an Amazon RDS instance for MySQL. Note that the password should be handled securely, especially in production environments.


### 5. Creating an IAM Role

```
provider "aws" {
  region = "us-west-2"
}

resource "aws_iam_role" "example" {
  name               = "example-role"
  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Action    = "sts:AssumeRole"
        Effect    = "Allow"
        Principal = {
          Service = "ec2.amazonaws.com"
        }
      },
    ]
  })

  tags = {
    Name = "ExampleRole"
  }
} 

```

This snippet defines an IAM role that can be assumed by EC2 instances. It includes a policy that allows EC2 to assume the role, which is essential for granting permissions to your resources.



Conclusion


These top five Terraform code snippets provide a solid foundation for managing cloud infrastructure. By utilizing these examples, you can efficiently deploy and manage resources in AWS, ensuring best practices in your infrastructure as code approach.