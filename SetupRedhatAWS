provider "aws" {
  region = "us-west-2"  # Change to your preferred AWS region
}

resource "aws_instance" "redhat_server" {
  ami           = "ami-0c55b159cbfafe1f0"  # Replace with a valid Red Hat Linux AMI ID for your region
  instance_type = "t2.micro"

  key_name = "my-key-pair"  # Replace with your key pair name

  tags = {
    Name = "RedHatServer"
  }

  # Security group to allow SSH access
  vpc_security_group_ids = [aws_security_group.allow_ssh.id]

  # User Data to set up Red Hat instance
  user_data = <<EOF
#!/bin/bash
# Add your Red Hat setup scripts here
EOF
}

resource "aws_security_group" "allow_ssh" {
  name        = "allow_ssh"
  description = "Allow SSH inbound traffic"

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]  # Allow SSH from anywhere (not recommended for production)
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
