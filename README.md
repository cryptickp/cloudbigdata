Description
==========

This is a Heat template to deploy a Rackspace Cloud Big Data cloud hadoop cluster.

Requirements
==========
* [python-heatclient](https://github.com/openstack/python-heatclient) `>= v0.2.8`:

```bash
pip install python-heatclient
```
* An Rackspace username, password, and tenant id.

We recommend installing the client within a [Python virtual
environment](http://www.virtualenv.org/).

Example Usage
=============
Here is an example of how to deploy this template using the
[python-heatclient](https://github.com/openstack/python-heatclient):

More CLI examples can be found in [README](https://github.com/rackerlabs/cbd_heat_plugin/blob/master/README.md)
##### Create a Heat Stack
```sh
heat --os-region-name <REGION> --os-auth-url https://identity.api.rackspacecloud.com/v2.0/ --os-tenant-id <TENANT-ID> --os-username <OS-USERNAME> --os-password <OS-PASSWORD> stack-create -f hadoop.yaml <CLUSTER-NAME>
```
Optionally, set environmental variables to avoid needing to provide these values every time a call is made:

```
export OS_USERNAME=<USERNAME>
export OS_PASSWORD=<PASSWORD>
export OS_TENANT_ID=<TENANT-ID>
export OS_AUTH_URL=<AUTH-URL>
```

Parameters
=========
Parameters can be replaced with your own values when standing up a stack.

 - `stackId`: Stack IDs define the type of CBD cluster to create. 
 - `clusterName`: A descriptive name of the cluster; useful when there are multiple clusters to track
 - `clusterLogin`: This will be the account created on the cluster to enable SSH access. Example: ssh clusterLogin@<your cluster IP>.
 - `flavor`: The flavor defines the resources (like disk space and RAM) available on the individual systems making up the cluster. Flavors are updated when new cloud hardware is available so it is always best to check the CBD REST API for the current list (see Reference Documentation below for details).
 - `numSlaveNodes`: numSlaveNodes defines the replication factor (how many copies of your data are stored for fault tolerance). 3 tends to be a pretty standard value. Higher replication will mean less total disk space available in the cluster and lower values may increase risk of data loss in rare catastrophic failure conditions.
 - `publicKeyName`: publicKeyName is an easy to remember name for the SSH public key used in the cluster. This name may be reused in other clusters in order to reuse public keys and allow the same private key to SSH into clusters across a company/organization if desired.
 - `publicKey` This is the full public key (matching your securely stored private key) that will be installed into the cluster systems which enable SSHing into cluster nodes. CBD clusters disable login/password-based SSH connections so this key is required for cluster access. It is important to put quotes around this value.

Outputs
=======

Once a stack comes online, use `heat output-list` to see all available outputs.
Use `heat output-show <OUTPUT NAME>` to get the value for a specific output.
 
 * `cluster_id`:  Cloud big data cluster ID.
 *  `cbd_version`: Current cloud big data version used.
 
Contributing
============
There are substantial changes still happening within the [OpenStack
Heat](https://wiki.openstack.org/wiki/Heat) project. Template contribution
guidelines will be drafted in the near future.

License
=======
```
Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

