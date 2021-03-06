.. _Network Stack Layer :

.. toctree::

###############################
VNET VPP Network Stack Layer
###############################

The files associated with the VPP network stack layer are located in the …/src/vnet folder. The Network Stack Layer is basically an instantiation of the code in the other layers. This layer has a vnet library that provides vectorized layer-2 and 3 networking graph nodes, a packet generator, and a packet tracer. 


In terms of building a packet processing application, vnet provides a
platform-independent subgraph to which one connects a couple of
device-driver nodes.

Typical RX connections include "ethernet-input" [full software
classification, feeds ipv4-input, ipv6-input, arp-input etc.] and
"ipv4-input-no-checksum" [if hardware can classify, perform ipv4
header checksum].

Effective graph dispatch function coding
----------------------------------------

Over the 15 years, two distinct styles have emerged: a
single/dual/quad loop coding model and a fully-pipelined coding
model. We seldom use the fully-pipelined coding model, so we won't
describe it in any detail.

Single/dual loops
-----------------

The single/dual/quad loop model is the only way to conveniently solve
problems where the number of items to process is not known in advance:
typical hardware RX-ring processing. This coding style is also very
effective when a given node will not need to cover a complex set of
dependent reads.

Below is a list of features and layer areas that VNET works with:

.. image:: /_images/VNET_Features.png
