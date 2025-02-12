# AWS IAM Data and Resources

Fog Security: https://www.fogsecurity.io/ 

Contact info@fogsecurity.io for help and feedback. Additions or feedback can be submitted here as well.

This repository contains information to help with tagging and tag compliance in AWS.   

## Tagging in AWS

For resources

### Full List of Tagging Actions in AWS

[json file of actions with 'tag' in the action](tagging/tagging_actions.json)
json structure: {service, action, access_level, description}

#### Explanation



#### Methodology





### Resources with support for aws:ResourceTag

[Resources with support for aws:ResourceTag](tagging/resources_with_aws:ResourceTag_support.json)
json structure: {service, resource, arn}

#### Explanation

**aws:ResourceTag/tag-key** is a property of the resource.  The tags of the target resource of the request are evaluated.  For example, we may want to write a policy that only allows an IAM principal to delete resources that have specific tags on them.  In this case, `aws:ResouceTag/tag-key` would be the condition we want to use.

#### Methodology 

We programmatically scanned through the Service Authorization pages of AWS IAM ([Actions, resources, and condition keys for AWS services](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)) and looked for at resource tables and pulled resource types that support `aws:ResourceTag/tag-key`.

`aws:ResourceTag/tag-key` ->  Supported Resources

#### When to Use

Use this condition key when ensuring that an action is only permitted on resources with a certain tag.  For example, only allowing an IAM principal permission to stop ec2 instances with a specific tag.


### Resources with support for aws:TagKeys 

[Resources with support for aws:TagKeys](tagging/resources_with_tagKeys_support.json)
json structure: {service, resource, arn}

#### Explanation

**aws:TagKeys** is a property of the request and not necessarily a property of the resouce in question.  An example of this is when creating a resource, `aws:TagKeys` can be used to limit which tags can be used when creating a resource.  

Note: We have seen inconsistencies for whether this is supported in certain AWS IAM Actions.  In some cases, `aws:TagKeys` is listed in the condition keys table on a service authorization page but is not present in the IAM Actions table.

#### Methodology 

We programmatically scanned through the Service Authorization pages of AWS IAM ([Actions, resources, and condition keys for AWS services](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)) and looked for at resource tables and pulled resource types that support `aws:TagKeys`.

`aws:TagKeys` -> IAM Action -> Supported Resources

#### When to use

Use this condition key when tags are required.  For example, ensuring that required tags are present when tagging a resource.  Note, this does not check to see what the tag key value may be.  To check for the tag key value in a request, we recommend using `aws:RequestTag/tag-key`.


### References

[AWS IAM: AWS Global Condition Context Keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html)

## References

https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-tagkeys
