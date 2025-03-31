# Ansible Jenkins Pipeline

This repository contains a Jenkins pipeline that runs Ansible in a Docker container.

## Files

- `Jenkinsfile`: The Jenkins pipeline definition
- `hello-world.yml`: A simple Ansible playbook that prints "Hello World" and creates an output file

## Requirements

- Jenkins with Docker installed
- Jenkins user must be in the Docker group

## Usage

1. Create a Jenkins pipeline job
2. Configure it to use this repository
3. Run the pipeline

## How it Works

The pipeline pulls the `alpine/ansible` Docker image and runs a simple Ansible playbook inside a container.
