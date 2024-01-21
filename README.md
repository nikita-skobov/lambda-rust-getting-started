an example repo for getting started with rust in AWS lambda.

## Why?

[lambda-runtime](https://github.com/awslabs/aws-lambda-rust-runtime) has instructions for using `cargo lambda build` to build lambda functions, however this is not necessary and this repository shows a minimal way to create rust executables ready to be ran in a lambda environment.

## Prerequisites

- docker (for cargo cross)
- [cargo cross](https://github.com/cross-rs/cross)
- rust
- zip
- AWS account to deploy to

## Usage

```sh
# build the executable (substitute x86_64 for aarch64 if not building for ARM)
cross build --target aarch64-unknown-linux-musl --release

# move the executable to current dir, and name it so AWS knows which file to execute
mv ./target/aarch64-unknown-linux-musl/release/lambda-rust-getting-started ./bootstrap

# package it for deployment. can include other files alongside bootstrap
zip -r my_deployment.zip bootstrap
```

- Now your deployment package is ready to be uploaded. go to your AWS Console > Lambda
- Create a new Lambda function. Choose Arm if you built for Arm, and choose lambda runtime v2.
- Once created scroll down to the "code source" panel and click "upload from" choose zip, and upload the `my_deployment.zip`

## Testing

Click on the "test" tab and invoke your lambda function with a sample event and see the output in the console.
