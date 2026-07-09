resource "aws_vpc" "my-vpc-1" {
    cidr_block = "10.0.0.0/16"
    tags= {
        Name="my-vpc-1"
    }
  
}
resource "aws_subnet" "private-subnet" {
    vpc_id = aws_vpc.my-vpc-1.id
    cidr_block = "10.0.1.0/24"
    availability_zone = "us-east-1"
    tags={
        Name="private-subnet"
    }
  
}
resource "aws_subnet" "public-subnet" {
    vpc_id = aws_vpc.my-vpc-1.id
    cidr_block = "10.0.2.0/24"
    availability_zone = "us-east-1"
    tags={
        Name="public-subnet"
    }
}

resource "aws_internet_gateway" "my-internet-gateway" {
    vpc_id = aws_vpc.my-vpc-1.id
    tags ={
        Name="my-internet-gateway"
    }
  
}
resource "aws_route_table" "public_rt" {
    vpc_id = aws_vpc.my-vpc-1.id
    route {
        cidr_block = "0.0.0.0/0"
        gateway_id=aws_internet_gateway.my-internet-gateway.id
    }
  
}
resource "aws_route_table" "private_rt" {
    vpc_id = aws_vpc.my-vpc-1.id
    route {
        cidr_block = "0.0.0.0/0"
        gateway_id=aws_internet_gateway.my-internet-gateway.id
    }
  
}
resource "aws_route_table_association" "public-associate" {
    route_table_id = aws_route_table.public_rt.id
    subnet_id = aws_subnet.public-subnet.id
  
}
resource "aws_route_table_association" "private-associate" {
    route_table_id = aws_route_table.private_rt.id
    subnet_id = aws_subnet.private-subnet.id
  
}
