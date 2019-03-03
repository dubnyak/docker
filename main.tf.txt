
provider "aws" {
        access_key = "${var.access_key}"
        secret_key = "${var.secrets_key}"
        region     = "${var.region}"
        profile    = "${var.profile}"
}


resource "aws_instance" "web" {
        instance_type = "t2.micro"
        ami           = "${var.ami}"

       associate_public_ip_address = "true"
        key_name   = "${var.key_name}"
         security_groups   = ["Test_SG"]


      user_data = "${data.template_file.user_data.rendered}"


tags {
    "Name"      = "${var.instance_name}"
   }
}



resource "aws_key_pair" "key_pair" {
    key_name   = "${var.key_name}"
    public_key = "${file(var.public_key_path)}"
}

resource "aws_security_group" "Test_SG" {
    name        = "Test_SG"
    vpc_id      = "${var.vpc_id}"

    egress {
        from_port       = 0
        to_port         = 0
        protocol        = "-1"
        cidr_blocks     = ["0.0.0.0/0"]
    }

    ingress {
        protocol    = "tcp"
        from_port   = 22
        to_port     = 22
        cidr_blocks = ["0.0.0.0/0"]
        description = "Allow SSH"
    }

    ingress {
        protocol    = "tcp"
        from_port   = 80
        to_port     = 80
        cidr_blocks = ["0.0.0.0/0"]
        description = "Allow HTTP"
    }

    ingress {
        protocol    = "tcp"
        from_port   = 443
        to_port     = 443
        cidr_blocks = ["0.0.0.0/0"]
        description = "Allow HTTPS"
    }
}



data "template_file" "user_data" {
template = "${file("~/userdata.sh")}"
}
