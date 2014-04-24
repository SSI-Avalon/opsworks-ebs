# Opswork EBS

This cookbook allows to describe and configure the EBS volumes attached to an instance.


## Extraction

This cookbook was extracted from the [AWS Opsworks cookbooks](https://github.com/aws/opsworks-cookbooks).

Unfortunately the way AWS releases and manages this repository does allow an easy integration with Berkshelf.
The different options to use the `ebs` cookbook were to:

 1. commit the complete Opswork repository in our Chef repo
 1. commit the `ebs` cookbook in our Chef repo
 1. extract the `ebs` cookbook in its own separate repo
 
 The first 2 options will make tracking upstream changes complicated, so #3 was used.
 
 ### How to create the `opswork-ebs` repo?
 
 ```bash
 git clone https://github.com/aws/opsworks-cookbooks.git
 mv opsworks-{cookbooks,ebs}
 cd opsworks-ebs
 git remote rm origin
 
 git filter-branch --tag-name-filter cat --prune-empty --subdirectory-filter ebs HEAD
 
 
 git tag -a srev_v1.0.0 -m srev_v1.0.0
 
 git remote add origin git@github.com:SSI-Avalon/opsworks-ebs.git
 
 
 git push
 
 ```

## Usage

In your Berksfile, now you can add:
```
cookbook 'ebs', :github => 'SSI-Avalon/opsworks-ebs'
```

And use the recipes like so:

```
include_recipe 'ebs::volumes`
```
