# PBCore.org website documentation

## General Info

PBCore.org is an informational website that provides documentation about the PBCore metadata schema. It is a WordPress site that is hosted with Amazon Web Services (AWS), and jointly maintained by the Media Library and Archives (MLA) department at WGBH in Boston, MA.

This documentation is for the administrators of the pbcore.org website, and the infrastructure used to run it.

## Website content

Content for the PBCore.org website is created within WordPress, primarily using "Pages" (as opposed to "Posts").

More more inforamtion on managing the content of the pbcore.org website, contact a [website admin](#user-content-website-admins)

## Webserver details

The website runs on an EC2 instance in AWS. It uses the fairly standard LAMP stack, consisting of the Amazon Linux operating system, Apache webserver, MySQL database, and PHP.

## Starting, Stopping, Rebooting the EC2 instance from the web

**Before you start:** This requires that you have an account with the proper permissions. To set one up, contact an [AWS admin](#user-content-aws-admins).

  1. Go to the [**EC2 Console**](https://console.aws.amazon.com/ec2/v2/home?region=us-east-1#). If you are not currently logged in, you will have to enter your username and password on [the login page for the WGBH AWS account](https://wgbh-mla.signin.aws.amazon.com/console) first.

  1. Follow the AWS documentation on how to [**Reboot Your Instance**](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-reboot.html). The EC2 instance for pbcore.org is named "PBCore prod". In addition to rebooting a running instance you may choose to:
    * **Stop** (if the instance is running)
    * **Start** (if the instance is not running)
    * **Terminate** - Terminating the instance will delete the instance completely, along with all the data, and will have to be restored from a saved image, provided one exists. Do not terminate the instance unless you know exactly what you're doing.


## Creating snapshots / images

**_TODO_**

## Restoring the EC2 instance

**_TODO_**

## Status Check Alarm

There is currently a Status Check Alarm that is sent to pbcoreinfo@wgbh.org whenever the EC2 instance is unreachable for 30 minutes.

In this case, "unreachable" means that AWS found the instance to be in a state of **StatusCheckFailed**, which essentially means it could not be pinged.

This is a very basic alarm, and does not indicate other problems that may prevent the website from functioning properly. For instance, if the database service quits unexpectedly, then the website will not function properly, however this particular alarm will not be triggered.

Also, this alarm does not indicate what the underlying problem might be. Diagnosing the real problem requires further digging.

To modify alarms and notifications, contact an [AWS admin](#user-content-aws-admins).

  > **NOTE:** While the alarm is configured to trigger only after 30 minutes of the instance being unreachable, it seems to actually trigger if the server is unreachable after only short periods of time. We're not sure why this happens, and it's not necessarily a bad thing. But it means that if you are momentarily stopping/starting the server, you may get an alarm notification.

## DNS and Elastic IP address

The DNS record for **pbcore.org** is managed by IT staff at WGBH (not part of the MLA). The DNS record points to an Elastic IP address, which is attached to the `PBCore prod` EC2 instance.

The means that if the `PBCore prod` instance is terminated, and replaced with a new instance (e.g. restored from a backup image), then the Elastic IP must also be re-attached to the new instance.

For any changes to the Elastic IP, or DNS configuration, contact an [AWS admin](#user-content-aws-admins).

## Login to EC2 instance with SSH (Advanced)

Logging into the EC2 instance using SSH requires access to the public/private key pair for 

## Contacts

##### AWS administrators for MLA at WGBH<a name="aws-admins"></a>

  * Chuck McCallum - chuck_mccallum@wgbh.org
  * Andrew Myers - andrew_myers@wgbh.org

##### PBCore.org website administrators<a name="website-admins"></a>

  * Lauren Sorensen - **_TODO: ok to put your email here?_**
  * Ryan Edge - **_TODO: ok to put your email here?_**
  * Rebecca Fraimow - rebecca_fraimow@wgbh.org