# cloudformation-static-site [![Build Status](https://travis-ci.org/EastCoastProduct/cloudformation-static-site.png)](https://travis-ci.org/EastCoastProduct/cloudformation-static-site)
Cloudformation script to set up static site hosting on AWS with S3 and Cloudfront

This is cloudformation script that gets you up and running for hosting a static website on S3 and making it even faster behind CloudFront. After cloudformation stack is successfully created you are all set up on AWS to host static page. Root file is set to index.html on that bucket, so your page will need to have index.html root file or you can update the scripts to change it.

Only thing you need to do  is to sync your static page directory on s3 bucket with index.html as root.

## steps to make it work

1. only manual step is to create hosted zone for your domain on route53 if you don't use route53 for your site already, you'll need to however if you want to achieve this (remember to transfer your existing DNS records to reoute53)
2. modify files in config, you need to put your domain in params.yml (hosted zone) and you can change stack name in config.yml as you'll probably want different stack name, [www_to_root](#www_to_root) option is explained separately
3. install packages needed for script to run using pip install <package>
  1. boto - and configure boto with your aws keys [Boto config](http://boto.readthedocs.org/en/latest/boto_config_tut.html)
  2. troposphere - cloudformation templates are written in it
4. thats it, just run the script `python cfn.py --create`
  * `-c` or `--create` is to flag that its to create the stack if you need to update it later just leave that flag out

Thats it, you are now all set up to host static site on AWS S3 and CloudFront. Only thing left to do is to get your files on that bucket.

You can also check the [static-site-bootstrap](https://github.com/EastCoastProduct/static-site-bootstrap) that has pretty nice example of getting started with static site structure.

## www_to_root<a name="www_to_root"></a>

This option gives a choice to pick between having root domain redirect to www subdomain or vice versa. For example if www_to_root is set to true requests to www.example.com will be redirected to example.com and if its set to false requests to example.com will be redirected to www.example.com.

Depending on which option is used CloudFront is set up to use different S3 bucket to serve files. If set to true and main domain is root domain its using that S3 bucket (example.com bucket).

If set to false and www subdomain is main its using www.example.com bucket to serve the files, so use buckets to upload files according to this settings.
