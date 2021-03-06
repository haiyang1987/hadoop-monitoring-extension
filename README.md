AppDynamics Apache Hadoop Monitoring Extension
==============================================

This extension works only with the standalone machine agent.

Use Case
-----------
The Hadoop monitoring extension captures metrics from Hadoop Resource Manager and/or Apache Ambari and displays them in AppDynamics Metric Browser.

Metrics include:
- Hadoop Resource Manager
  - App status and progress
  - Memory usage
  - Container usage and status
  - Node count and status
  - Scheduler capacity, app and container count
- Ambari
  - Individual host metrics including CPU, disk, memory, JVM, load, network, process, and RPC metrics
  - Service metrics for HDFS, YARN, MapReduce, HBase, Hive, WebHCat, Oozie, Ganglia, Nagios, and ZooKeeper


Installation
-------------
#### Prerequisites
- Hadoop distribution that features Hadoop YARN. Distributions based on Hadoop 2.x should include YARN
	- Examples: hadoop-2.x, hadoop-0.23.x, CDH4 from Cloudera, HDP 2 from Hortonworks, and Pivotal HD from Pivotal
- Resource Manager hostname and port  
OR
- Any release of Apache Amabri
- Any version of Hadoop cluster installed via Ambari
- Ambari server hostname, port, username, and password

If the cluster version is 1.x and not installed by Ambari, no metrics can be gathered at this time.

#### Steps
1. Run `mvn clean install` from the hadoop-monitoring-extension directory.
2. Deploy the file HadoopMonitor.zip found in the 'target' directory into \<machineagent install dir>/monitors/.
3. Unzip the deployed file.
4. Open \<machineagent install dir>/monitors/HadoopMonitor/monitor.xml and configure the HRM and/or Ambari parameters.
5. (Optional, recommended) For metric filtering, configure  \<machineagent install dir>/monitors/HadoopMonitor/properties.xml.
6. Restart the machine agent.
7. In the AppDynamics Metric Browser, look for: Application Infrastructure Performance | \<Tier> | Custom Metrics | Hadoop.

Metrics
------------
### Hadoop Resource Manager: 
http://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/ResourceManagerRest.html
#### Apps
Metrics under Apps are aggregated metrics from all running and recently finished apps. To specify the period for which metrics are gathered, set \<aggregate-app-period> in properties.xml.


### Ambari

#### Host Metrics

| Metric Name   | Description
|---------------|----------------
| cpu           | CPU usage
| disk          | Disk usage (GB)
| jvm           | JVM log message count, memory usage, and thread count
| load          | Host load in 15, 5, and 1 min averages
| memory        | Memory usage (KB)
| network       | Bytes in/out, packets in/out
| process       | Process count
| rpc           | RPC process time, queue time, sent and received bytes
| rpcdetailed   | Additional RPC metrics
| ugi           | User Group Information
| part_max_used | Percent disk usage
| state         | Host state

#### Service Specific Metrics

| Metric Name   | Description
|---------------|----------------
| dfs           | HDFS specific metrics
| yarn          | YARN specific metrics
| mapred        | MapReduce specific metrics
| hbase         | HBase specific metrics

#### Host States

| State                           | Value | Description
|---------------------------------|-------|--------------
| INIT                            | 0     | New host state.
| WAITING_FOR_HOST_STATUS_UPDATES | 1     | Registration request is received from the Host but the host has not responded to its status update check.
| HEALTHY                         | 2     | The server is receiving heartbeats regularly from the host and the state of the host is healthy.
| HEARTBEAT_LOST                  | 3     | The server has not received a heartbeat from the host in the configured heartbeat expiry window.
| UNHEALTHY                       | 4     | Host is in unhealthy state as reported either by the Host itself or via any other additional means ( monitoring layer ).

#### Service States

| State           | Value | Description
|-----------------|-------|----------------
| INIT            | 0     | The initial clean state after the service is first created.
| INSTALLING      | 1     | In the process of installing the service.
| INSTALL_FAILED  | 2     | The service install failed.
| INSTALLED       | 3     | The service has been installed successfully but is not currently running.
| STARTING        | 4     | In the process of starting the service.
| STARTED         | 5     | The service has been installed and started.
| STOPPING        | 6     | In the process of stopping the service.
| UNINSTALLING    | 7     | In the process of uninstalling the service.
| UNINSTALLED     | 8     | The service has been successfully uninstalled.
| WIPING_OUT      | 9     | In the process of wiping out the installed service.
| UPGRADING       | 10    | In the process of upgrading the service.
| MAINTENANCE     | 11    | The service has been marked for maintenance.
| UNKNOWN         | 12    | The service state can not be determined.

#### Service component

| Metric Name | Description
|-------------|----------------
| CPU         | CPU usage
| Disk        | Disk usage (GB)
| JVM         | JVM log message count, memory usage, and thread count
| Load        | Component load in 15, 5, and 1 min averages
| Memory      | Memory usage (KB)
| Network     | Bytes in/out, packets in/out
| Process     | Process count
| RPC         | RPC process time, queue time, sent and received bytes
| RPCdetailed | Additional RPC metrics
| UGI         | User Group Information
| State       | Component state

#### Service Component States

|State           | Value | Description
|----------------|-------|-------------
|INIT            | 0     | The initial clean state after the component is first created.
|INSTALLING      | 1     | In the process of installing the component.
|INSTALL_FAILED  | 2     | The component install failed.
|INSTALLED       | 3     | The component has been installed successfully but is not currently running.
|STARTING        | 4     | In the process of starting the component.
|STARTED         | 5     | The component has been installed and started.
|STOPPING        | 6     | In the process of stopping the component.
|UNINSTALLING    | 7     | In the process of uninstalling the component.
|UNINSTALLED     | 8     | The component has been successfully uninstalled.
|WIPING_OUT      | 9     | In the process of wiping out the installed component.
|UPGRADING       | 10    | In the process of upgrading the component.
|MAINTENANCE     | 11    | The component has been marked for maintenance.
|UNKNOWN         | 12    | The component state can not be determined.

Custom Dashboard
------------------
#### Hadoop 1

![](https://raw.github.com/Appdynamics/hadoop-monitoring-extension/master/HadoopDashboard.png)

#### Hadoop 2

![](https://raw.github.com/Appdynamics/hadoop-monitoring-extension/master/Hadoop2Dashboard.png)

Contributing
------------

Always feel free to fork and contribute any changes directly via <a href="https://github.com/Appdynamics/hadoop-monitoring-extension">GitHub</a>.


Community
---------

Find out more in the <a href="http://appsphere.appdynamics.com/t5/eXchange/Hadoop-Monitoring-Extension/idi-p/3583">AppSphere</a>.

Support
-------

For any questions or feature request, please contact <a href="mailto:ace-request@appdynamics.com">AppDynamics Center of Excellence</a>.

