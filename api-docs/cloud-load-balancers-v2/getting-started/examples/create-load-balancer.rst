.. _create-load-balancer:

==========================
Creating a load balancer
==========================

Cloud Load Balancers make it easy to develop scalable, high-availability
configurations in the Cloud. By leveraging Cloud Load Balancers, you
will be provided with a dedicated IP address that you can use to reach
your service.

You need to use the Create Load Balancer API call (``POST /loadbalancers``)
to create a load balancer with the configuration that you specify.

In this case, assume that you want to create a load balancer with the
following configuration:

-  name = "loadbalancer1"

-  description = "simple lb"

-  vip\_subnet\_id = "**your\_vip\_subnet\_id**"

   The UUID of the subnet on which to allocate the virtual IP (VIP)
   address. The ``vip_subnet_id`` is the id of a subnet returned from
   querying neutron's subnets as follows:
   ``neutron.endpoint/v2.0/subnets?shared=True``

   **Reviewer: please specify the specific \ ``neutron.endpoint``\ 
   mentioned in the previous sentence.**

-  vip\_address = "10.0.0.4"

   The IP address of the VIP.

      style="margin-left: 0.5in; margin-right: 0.5in;">

   ..  note:: 
     This field is optional. It currently cannot be provided. Omit it to
     have the system provide the VIP.

-  admin\_state\_up = "true"

   Specify that the admin state for the new load balancer is up (true).

The following example shows the cURL request for Create Load Balancer:

**Example. cURL Create Load Balancer Request: JSON**

.. code::  

    curl -s -d \
    '{
        "loadBalancer": {
            "name": "loadbalancer1",
            "description": "simple lb",
            "vip_subnet_id": "your_vip_subnet_id",
            "admin_state_up": true    
         }
    }' \
    -H "X-Auth-Token: $AUTH_TOKEN" \
    -H "Content-Type: application/json" \
    "$API_ENDPOINT/loadbalancers" | python -m json.tool

Remember to replace the names in the examples above with their actual
respective values for all the cURL examples that follow:

-  **your\_auth\_token** — as returned in your authentication response
   (see the response examples in `Chapter 4, *Generate an authentication
   token* <Generating_Auth_Token.html>`__)

-  **your\_vip\_subnet\_id** — The UUID of the subnet on which to
   allocate the virtual IP (VIP) address.

The following example shows the response for Create load balancer:

**Example. cURL Create Load Balancer Response: JSON**

.. code::  

    {
      "loadbalancer": {
        "admin_state_up": true,
        "description": "simple lb",
        "id": "a36c20d0-18e9-42ce-88fd-82a35977ee8c",
        "listeners": [
          
        ],
        "name": "loadbalancer1",
        "operating_status": "ONLINE",
        "provisioning_status": "ACTIVE",
        "tenant_id": "b7c1a69e88bf4b21a8148f787aef2081",
        "vip_address": "10.0.0.4",
        "vip_subnet_id": "013d3059-87a4-45a5-91e9-d721068ae0b2"
      }
    }

In the previous examples, you can see that a new load balancer has been
created with id a36c20d0-18e9-42ce-88fd-82a35977ee8c. You will need the
load balancer id for making the Show load balancer details call in the
next section, and you should supply this value wherever you see the
field **load\_balancer\_id** in the examples in this guide.
