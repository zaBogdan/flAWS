# flAWS.cloud - A vulnerable AWS cloud environment

### TL;DR

### Part 1 - First interaction with AWS CLI and S3 buckets

--- to be removed
if we ping `flaws.cloud` -> we get `s3-website-us-west-2.amazonaws.com` meaning we have to deal with an S3 bucket-> we can run `aws s3 ls s3://flaws.cloud --no-sign-request --region us-west-2` -> leaks `secret-dd02c7c.html` which leaks the second domain `http://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud`

### Part 2 - Free for all 

--- to be removed
We have to create an AWS account -> Get Access and secret key -> create a profile with `aws configure` -> use the command `aws s3 ls s3://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud/ --profile default --region us-west-2` -> leaks `secret-e4443fc.html` -> leaking `http://level3-9afd3927f195e10225021a578e6f78df.flaws.cloud`

### Part 3 - Wait? What key?

--- to be removed
If we least the level3 bucket with `aws s3 ls s3://level3-9afd3927f195e10225021a578e6f78df.flaws.cloud --profile default --region us-west-2` -> we get a `.git` folder -> using git-dumper -> git log -> there is a commit called `Oops, accidentally added something I shouldn't have` -> so we checkout to the previous commit with `git checkout f52ec03b227ea6094b04e43f475fb0126edb5a61` -> with the access keys we can create a new profile in `~/.aws/credentials` -> we querry to see all domains with `aws s3 --profile flaws ls` -> we now have all levels leaked.
```
[flaws]
aws_access_key_id = AKIAJ366LIPB4IJKT7SA
aws_secret_access_key = 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
```
 
### Part 4 - Now we have a VM!
