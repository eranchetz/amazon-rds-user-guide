# Viewing key monitoring information<a name="accessing-monitoring"></a>

The Amazon RDS console provides quick access to key monitoring features\.

**Topics**
+ [Viewing DB instance status](#Overview.DBInstance.Status)
+ [Viewing Amazon RDS recommendations](#USER_Recommendations)
+ [Viewing DB instance metrics](#USER_Monitoring)

## Viewing DB instance status<a name="Overview.DBInstance.Status"></a>

The status of a DB instance indicates the health of the DB instance\. You can view the status of a DB instance by using the Amazon RDS console, the AWS CLI command [describe\-db\-instances](https://docs.aws.amazon.com/cli/latest/reference/rds/describe-db-instances.html), or the API operation [DescribeDBInstances](https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DescribeDBInstances.html)\. 

**Note**  
Amazon RDS also uses another status called *maintenance status*, which is shown in the **Maintenance** column of the Amazon RDS console\. This value indicates the status of any maintenance patches that need to be applied to a DB instance\. Maintenance status is independent of DB instance status\. For more information on *maintenance status*, see [Applying updates for a DB instance](USER_UpgradeDBInstance.Maintenance.md#USER_UpgradeDBInstance.OSUpgrades)\. 

Find the possible status values for DB instances in the following table\. This table also shows whether you will be billed for the DB instance and storage, billed only for storage, or not billed\. For all DB instance statuses, you are always billed for backup usage\.


| DB instance status | Billed  | Description | 
| --- | --- | --- | 
|  **available**  | Billed |  The DB instance is healthy and available\.  | 
|  **backing\-up**  | Billed |  The DB instance is currently being backed up\.  | 
|  **configuring\-enhanced\-monitoring**  | Billed |  Enhanced Monitoring is being enabled or disabled for this DB instance\.  | 
|  **configuring\-iam\-database\-auth**  | Billed |  AWS Identity and Access Management \(IAM\) database authentication is being enabled or disabled for this DB instance\.  | 
|  **configuring\-log\-exports**  | Billed |  Publishing log files to Amazon CloudWatch Logs is being enabled or disabled for this DB instance\.  | 
|  **converting\-to\-vpc**  | Billed |  The DB instance is being converted from a DB instance that is not in an Amazon Virtual Private Cloud \(Amazon VPC\) to a DB instance that is in an Amazon VPC\.  | 
|  **creating**  | Not billed |  The DB instance is being created\. The DB instance is inaccessible while it is being created\.   | 
|  **deleting**  | Not billed |  The DB instance is being deleted\.  | 
|  **failed**  | Not billed |  The DB instance has failed and Amazon RDS can't recover it\. Perform a point\-in\-time restore to the latest restorable time of the DB instance to recover the data\.   | 
|  **inaccessible\-encryption\-credentials**  | Not billed |  The AWS KMS customer master key \(CMK\) used to encrypt or decrypt the DB instance can't be accessed\.   | 
|  **incompatible\-network**  | Not billed |  Amazon RDS is attempting to perform a recovery action on a DB instance but can't do so because the VPC is in a state that prevents the action from being completed\. This status can occur if, for example, all available IP addresses in a subnet are in use and Amazon RDS can't get an IP address for the DB instance\.   | 
|  **incompatible\-option\-group**  | Billed |  Amazon RDS attempted to apply an option group change but can't do so, and Amazon RDS can't roll back to the previous option group state\. For more information, check the **Recent Events** list for the DB instance\. This status can occur if, for example, the option group contains an option such as TDE and the DB instance doesn't contain encrypted information\.   | 
|  **incompatible\-parameters**  | Billed |  Amazon RDS can't start the DB instance because the parameters specified in the DB instance's DB parameter group aren't compatible with the DB instance\. Revert the parameter changes or make them compatible with the DB instance to regain access to your DB instance\. For more information about the incompatible parameters, check the **Recent Events** list for the DB instance\.   | 
|  **incompatible\-restore**  | Not billed |  Amazon RDS can't do a point\-in\-time restore\. Common causes for this status include using temp tables, using MyISAM tables with MySQL, or using Aria tables with MariaDB\.  | 
| insufficient\-capacity |  |  Amazon RDS can’t create your instance because sufficient capacity isn’t currently available\. To create your DB instance in the same AZ with the same instance type, delete your DB instance, wait a few hours, and try to create again\. Alternatively, create a new instance using a different instance class or AZ\.  | 
|  **maintenance**  | Billed |  Amazon RDS is applying a maintenance update to the DB instance\. This status is used for instance\-level maintenance that RDS schedules well in advance\.   | 
|  **modifying**  | Billed |  The DB instance is being modified because of a customer request to modify the DB instance\.   | 
|  **moving\-to\-vpc**  | Billed |  The DB instance is being moved to a new Amazon Virtual Private Cloud \(Amazon VPC\)\.  | 
|  **rebooting**  | Billed |  The DB instance is being rebooted because of a customer request or an Amazon RDS process that requires the rebooting of the DB instance\.  | 
|  **resetting\-master\-credentials**  | Billed |  The master credentials for the DB instance are being reset because of a customer request to reset them\.  | 
|  **renaming**  | Billed |  The DB instance is being renamed because of a customer request to rename it\.   | 
|  **restore\-error**  | Billed |  The DB instance encountered an error attempting to restore to a point\-in\-time or from a snapshot\.  | 
|  **starting**  | Billed for storage |  The DB instance is starting\.  | 
|  **stopped**  | Billed for storage |  The DB instance is stopped\.  | 
|  **stopping**  | Billed for storage |  The DB instance is being stopped\.  | 
|  **storage\-full**  | Billed |  The DB instance has reached its storage capacity allocation\. This is a critical status, and we recommend that you fix this issue immediately\. To do so, scale up your storage by modifying the DB instance\. To avoid this situation, set Amazon CloudWatch alarms to warn you when storage space is getting low\.   | 
|  **storage\-optimization**  | Billed |  Your DB instance is being modified to change the storage size or type\. The DB instance is fully operational\. However, while the status of your DB instance is **storage\-optimization**, you can't request any changes to the storage of your DB instance\. The storage optimization process is usually short, but can sometimes take up to and even beyond 24 hours\.   | 
|  **upgrading**  | Billed |  The database engine version is being upgraded\.   | 

## Viewing Amazon RDS recommendations<a name="USER_Recommendations"></a>

Amazon RDS provides automated recommendations for database resources, such as DB instances, read replicas, and DB parameter groups\. These recommendations provide best practice guidance by analyzing DB instance configuration, usage, and performance data\.

You can find examples of these recommendations in the following table\.


| Type | Description | Recommendation | Additional information | 
| --- | --- | --- | --- | 
|  Engine version outdated  |  Your DB instance is not running the latest minor engine version\.  |  We recommend that you upgrade to the latest version because it contains the latest security fixes and other improvements\.  |  [Upgrading a DB instance engine version](USER_UpgradeDBInstance.Upgrading.md)  | 
|  Pending maintenance available  |  You have pending maintenance available on your DB instance\.  |  We recommend that you perform the pending maintenance available on your DB instance\. Updates to the operating system most often occur for security issues and should be done as soon as possible\.  |  [Maintaining a DB instance](USER_UpgradeDBInstance.Maintenance.md)  | 
|  Automated backups disabled  |  Your DB instance has automated backups disabled\.  |  We recommend that you enable automated backups on your DB instance\. Automated backups enable point\-in\-time recovery of your DB instance\. You receive backup storage up to the storage size of your DB instance at no additional charge\.  |  [Working with backups](USER_WorkingWithAutomatedBackups.md)  | 
|  Magnetic volumes in use  |  Your DB instance is using magnetic storage\.  |  Magnetic storage is not recommended for most DB instances\. We recommend switching to General Purpose \(SSD\) storage or provisioned IOPS storage\.  |  [Amazon RDS DB instance storage](CHAP_Storage.md)  | 
|  EC2\-Classic platform in use  |  Your DB instance is using the legacy EC2\-Classic platform\.  |  We recommend moving your DB instance to the EC2\-VPC platform for better network access control\. Amazon VPC provides a virtual network that is logically isolated from other virtual networks in the AWS Cloud\.  |  [Determining whether you are using the EC2\-VPC or EC2\-Classic platform](USER_VPC.FindDefaultVPC.md)  | 
|  Enhanced Monitoring disabled  |  Your DB instance doesn't have Enhanced Monitoring enabled\.  |  We recommend enabling Enhanced Monitoring\. Enhanced Monitoring provides real\-time operating system metrics for monitoring and troubleshooting\.  |  [Tracking OS metrics using Enhanced Monitoring](USER_Monitoring.OS.md)  | 
|  Encryption disabled  |  Your DB instance doesn't have encryption enabled\.  |  We recommend enabling encryption\. You can encrypt your existing Amazon RDS DB instances by restoring from an encrypted snapshot\.  |  [Encrypting Amazon RDS resources](Overview.Encryption.md)  | 
|  Previous generation DB instance class in use  |  Your DB instance is running on a previous\-generation DB instance class\.  |  Previous\-generation DB instance classes have been replaced by DB instance classes with better price, better performance, or both\. We recommend running your DB instance on a later generation DB instance class\.  |  [DB instance classes](Concepts.DBInstanceClass.md)  | 
|  Huge pages not used for an Oracle DB instance  |  The `use_large_pages` parameter is not set to `ONLY` in the DB parameter group used by your DB instance\.  |  For increased database scalability, we recommend setting `use_large_pages` to `ONLY` in the DB parameter group used by your DB instance\.  |  [Enabling HugePages for an Oracle DB instance](Appendix.Oracle.CommonDBATasks.Misc.md#Oracle.Concepts.HugePages)  | 
|  Nondefault custom memory parameters  |  Your DB parameter group sets memory parameters that diverge too much from the default values\.  |  Settings that diverge too much from the default values can cause poor performance and errors\. We recommend setting custom memory parameters to their default values in the DB parameter group used by the DB instance\.  |  [Working with DB parameter groups](USER_WorkingWithParamGroups.md)  | 
|  Change buffering enabled for a MySQL DB instance  |  Your DB parameter group has change buffering enabled\.  |  Change buffering allows a MySQL DB instance to defer some writes necessary to maintain secondary indexes\. This configuration can improve performance slightly, but it can create a large delay in crash recovery\. During crash recovery, the secondary index must be brought up to date\. So, the benefits of change buffering are outweighed by the potentially very long crash recovery events\. We recommend disabling change buffering\.  |  [ Best practices for configuring parameters for Amazon RDS for MySQL, part 1: Parameters related to performance](http://aws.amazon.com/blogs/database/best-practices-for-configuring-parameters-for-amazon-rds-for-mysql-part-1-parameters-related-to-performance/) on the AWS Database Blog  | 
|  Query cache enabled for a MySQL DB instance  |  Your DB parameter group has query cache parameter enabled\.  |  The query cache can cause the DB instance to appear to stall when changes require the cache to be purged\. Most workloads don't benefit from a query cache\. The query cache was removed from MySQL version 8\.0\. We recommend that you disable the query cache parameter\.  |  [ Best practices for configuring parameters for Amazon RDS for MySQL, part 1: Parameters related to performance](http://aws.amazon.com/blogs/database/best-practices-for-configuring-parameters-for-amazon-rds-for-mysql-part-1-parameters-related-to-performance/) on the AWS Database Blog  | 
|  Logging to table  |  Your DB parameter group sets logging output to `TABLE`\.  |  Setting logging output to `TABLE` uses more storage than setting this parameter to `FILE`\. To avoid reaching the storage limit, we recommend setting the logging output parameter to `FILE`\.  |  [Accessing MySQL database log files](USER_LogAccess.Concepts.MySQL.md)  | 

Amazon RDS generates recommendations for a resource when the resource is created or modified\. Amazon RDS also periodically scans your resources and generates recommendations\.

### Responding to Amazon RDS recommendations<a name="USER_Recommendations.Responding"></a>

You can find recommendations in the AWS Management Console\. You can perform the recommended action immediately, schedule it for the next maintenance window, or dismiss it\.

**To respond to Amazon RDS recommendations**

1. Sign in to the AWS Management Console and open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Recommendations**\.  
![\[Select Recommendations in the console\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/recommendations-select.png)

   The Recommendations page appears\.  
![\[Main Recommendations page in the console\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/recommendations-main.png)

1. On the **Recommendations** page, choose one of the following:
   + **Active** – Shows the current recommendations that you can apply, dismiss, or schedule\.
   + **Dismissed** – Shows the recommendations that have been dismissed\. When you choose **Dismissed**, you can apply these dismissed recommendations\.
   + **Scheduled** – Shows the recommendations that are scheduled but not yet applied\. These recommendations will be applied in the next scheduled maintenance window\.
   + **Applied** – Shows the recommendations that are currently applied\.

   From any list of recommendations, you can open a section to view the recommendations in that section\.  
![\[Take action on recommendations in the console\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/recommendations-active.png)

   To configure preferences for displaying recommendations in each section, choose the **Preferences** icon\.  
![\[Preferences icon for Recommendations in the console\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/recommendations-preferences.png)

   From the **Preferences** window that appears, you can set display options\. These options include the visible columns and the number of recommendations to display on the page\.

1. Manage your active recommendations:

   1. Choose **Active** and open one or more sections to view the recommendations in them\.

   1. Choose one or more recommendations and choose **Apply now** \(to apply them immediately\), **Schedule** \(to apply them in next maintenance window\), or **Dismiss**\.

      If the **Apply now** button appears for a recommendation but is unavailable \(grayed out\), the DB instance is not available\. You can apply recommendations immediately only if the DB instance status is **available**\. For example, you can't apply recommendations immediately to the DB instance if its status is **modifying**\. In this case, wait for the DB instance to be available and then apply the recommendation\.

      If the **Apply now** button doesn't appear for a recommendation, you can't apply the recommendation using the **Recommendations** page\. You can modify the DB instance to apply the recommendation manually\.

      For more information about modifying a DB instance, see [Modifying an Amazon RDS DB instance](Overview.DBInstance.Modifying.md)\.
**Note**  
When you choose **Apply now**, a brief DB instance outage might result\.

## Viewing DB instance metrics<a name="USER_Monitoring"></a>

Amazon RDS provides metrics so that you can monitor the health of your DB instances\. You can monitor both DB instance metrics and operating system \(OS\) metrics\.

Following, you can find details about how to view metrics for your DB instance using the RDS console and CloudWatch\. For information on monitoring metrics for your DB instance's operating system in real time using CloudWatch Logs, see [Tracking OS metrics using Enhanced Monitoring](USER_Monitoring.OS.md)\.

### Viewing metrics by using the console<a name="USER_Monitoring.CON"></a>

**To view DB and OS metrics for a DB instance**

1. Sign in to the AWS Management Console and open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Databases**\.

1. Choose the name of the DB instance that you need information about to show its details\.

1. Choose the **Monitoring** tab\.

1. For **Monitoring**, choose the option for how you want to view your metrics from these:
   + **CloudWatch** – Shows a summary of DB instance metrics available from Amazon CloudWatch\. Each metric includes a graph showing the metric monitored over a specific time span\.
   + **Enhanced monitoring** – Shows a summary of OS metrics available for a DB instance with Enhanced Monitoring enabled\. Each metric includes a graph showing the metric monitored over a specific time span\.
   + **OS Process list** – Shows details for each process running in the selected instance\.
   + **Performance Insights** – Opens the Amazon RDS Performance Insights console for your DB instance\.

     
![\[RDS metrics viewing options\]](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/metrics0.png)
**Tip**  
To choose the time range of the metrics represented by the graphs, you can use the time range list\.  
To bring up a more detailed view, you can choose any graph\. You can also apply metric\-specific filters to the data\. 

### Viewing DB instance metrics with the CLI or API<a name="USER_Monitoring.DB"></a>

Amazon RDS integrates with CloudWatch metrics to provide a variety of DB instance metrics\. You can view CloudWatch metrics using the RDS console, AWS CLI, or API\.

 For a complete list of Amazon RDS metrics, go to [ Amazon RDS dimensions and metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/rds-metricscollected.html) in the *Amazon CloudWatch User Guide*\. 

#### Viewing DB metrics by using the CloudWatch CLI<a name="USER_Monitoring.CLI"></a>

**Note**  
The following CLI example requires the CloudWatch command line tools\. For more information on CloudWatch and to download the developer tools, see [Amazon CloudWatch](https://aws.amazon.com/cloudwatch) on the AWS website\. The `StartTime` and `EndTime` values supplied in this example are for illustration only\. Substitute appropriate start and end time values for your DB instance\.

**To view usage and performance statistics for a DB instance**
+ Use the CloudWatch command `mon-get-stats` with the following parameters\.

  ```
  1. PROMPT>mon-get-stats FreeStorageSpace --dimensions="DBInstanceIdentifier=mydbinstance" --statistics= Average 
  2.   --namespace="AWS/RDS" --start-time 2009-10-16T00:00:00 --end-time 2009-10-16T00:02:00
  ```

#### Viewing DB metrics by using the CloudWatch API<a name="USER_Monitoring.API"></a>

The `StartTime` and `EndTime` values supplied in this example are for illustration only\. Substitute appropriate start and end time values for your DB instance\.

**To view usage and performance statistics for a DB instance**
+ Call the CloudWatch API `GetMetricStatistics` with the following parameters:
  + `Statistics.member.1` = `Average`
  + `Namespace` = `AWS/RDS`
  + `StartTime` = `2009-10-16T00:00:00`
  + `EndTime` = `2009-10-16T00:02:00`
  + `Period` = `60`
  + `MeasureName` = `FreeStorageSpace`