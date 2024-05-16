# monolith-compile-upload-action

This action is intended to share a common set of steps we use to
compile and upload code for the monolith.

- Checkout the monolith code
- Restore NuGet packages
- Build
- Precompile websites
- Checkout AwsDeploy code
- Combine monolith and aws deploy code
- Upload 

## Parameters

#### 'github_ref_name' (required)
The GitHub property 'github.ref' that helps determine the branch name.

#### 'github_sha' (required)
The GitHub property 'github.sha' that provides a unique id.

#### 'custom_access_token' (required)
Access token for GitHub AwsDeploy repository.

#### 's3_bucket' (required)
S3 Bucket name

#### 's3_folder'
S3 Folder path. Optional

#### 'aws_access_key' (required)
Access key for Aws upload.

#### 'aws_secret_key' (required)
Secret key for Aws upload.

#### 'aws_region' (optional)
Aws region used. Default is 'us-east-1'.

## Sample Use

```
  compile-upload: 
    name:  Compile and Upload
    runs-on: psidev-windows
    steps:
    - name: "Monolith/AWS Compile and Upload"
      uses: patriotsoftware/monolith-compile-upload-action@v1
      with:
        github_ref_name: ${{ github.ref_name }}
        github_sha: ${{ github.sha }}
        s3_bucket: monolithdev-codedeploy
        s3_folder: suite   
        custom_access_token: ${{ secrets.CUSTOM_GITHUB_ACCESS_TOKEN }}
        aws_access_key: ${{ secrets.DEV_AWS_ACCESS_KEY_ID }}
        aws_secret_key: ${{ secrets.DEV_AWS_SECRET_ACCESS_KEY }}
```
