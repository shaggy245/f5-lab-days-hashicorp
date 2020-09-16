BIG-IP Infrastructure Onboarding
################################

In this section you will configure basic network configurations like NTP, DNS, and interface IP addresses.

#. Confirm BIG-IP is not configured with basic network configurations.

   - Explore BIG-IP GUI **Network SelfIP** and **Vlan** settings and validate they are not configured

   .. image:: /_static/selfip0.png
       :height: 150px

   .. image:: /_static/vlan0.png
       :height: 150px

#. Create **main.tf** to use the `[Terraform Provider for F5 BIG-IP] <https://registry.terraform.io/providers/F5Networks/bigip/latest/docs>`__

   - Open client server **vscode terminal**
   - ``mkdir ~/projects/lab1``
   - ``cd ~/projects/lab1``
   - ``touch main.tf``
   - use vscode to add the following code to **main.tf**

   .. code:: json

     terraform {
     required_providers {
       bigip = {
         source = "F5Networks/bigip"
         version = "1.3.1"
       }
     }
     }

     provider "bigip" {
       address = "10.1.1.6"
       username = "admin"
       password = "F5d3vops$"
     }

     resource "bigip_command" "showversion" {
       commands   = ["show sys version"]
     }

     output "showversion" {
       value = "${bigip_command.showversion.command_result}"
     }

   .. image:: /_static/maintf.png
       :height: 300px