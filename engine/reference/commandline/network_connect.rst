.. -*- coding: utf-8 -*-
.. https://docs.docker.com/engine/reference/commandline/network_connect/
.. doc version: 1.9
.. check date: 2015/12/27
.. -----------------------------------------------------------------------------

.. network connect

=======================================
network connect
=======================================

.. code-block:: bash

   Usage:  docker network connect [OPTIONS] NETWORK CONTAINER
   
   Connects a container to a network
   
     --help=false       Print usage

.. Connects a running container to a network. You can connect a container by name or by ID. Once connected, the container can communicate with other containers in the same network.

実行中のコンテナをネットワークに接続（connect）します。接続はコンテナ名か ID で行えます。一度接続すると、コンテナは同じネットワーク上の他のコンテナと通信できます。

.. code-block:: bash

   $ docker network connect multi-host-network container1

.. You can also use the docker run --net=<network-name> option to start a container and immediately connect it to a network.

あるいは、 ``docker run --net=<ネットワーク名>`` オプションを使うと、コンテナ起動時に、ただちにネットワークに接続します。

.. code-block:: bash

   $ docker run -itd --net=multi-host-network busybox

.. You can pause, restart, and stop containers that are connected to a network. Paused containers remain connected and a revealed by a network inspect. When the container is stopped, it does not appear on the network until you restart it. The container’s IP address is not guaranteed to remain the same when a stopped container rejoins the network.

コンテナを中断（pause）・再起動・停止しても、ネットワークに接続したままです。中断したコンテナはネットワークに接続しつづけており、 ``network inspect`` で確認できます。コンテナを停止（stop）すると、再起動するまではネットワーク上に表示されません。停止していたコンテナが再起動時、同じネットワークに参加しても IP アドレスが同じになる保証はありません。

.. To verify the container is connected, use the docker network inspect command. Use docker network disconnect to remove a container from the network.

コンテナがどこに接続しているかを確認するには、 ``docker network inspect`` コマンドを使います。 ``docker network disconnect`` はコンテナをネットワークから切り離します。

.. Once connected in network, containers can communicate using only another container’s IP address or name. For overlay networks or custom plugins that support multi-host connectivity, containers connected to the same multi-host network but launched from different Engines can also communicate in this way.

ネットワークに接続すると、コンテナは他のコンテナの IP アドレスや名前を使って通信できるようになります。 ``overlay`` ネットワークやカスタム・プラグインは複数のホスト間の接続性（multi-host connectivity）をサポートしています。コンテナは同じマルチホスト・ネットワーク上で接続できるだけではありません。異なったエンジンによって起動されていたとしても、同様に通信できます。

.. You can connect a container to one or more networks. The networks need not be the same type. For example, you can connect a single container bridge and overlay networks.

コンテナは複数のネットワークにも接続できます。ネットワークは同じ種類でなくても構いません。例えば、コンテナ・ブリッジとオーバレイ・ネットワークの両方に接続できます。

.. Related information

.. _network-connect-related-information:

関連情報
==========

..    network inspect
    network create
    network disconnect
    network ls
    network rm
    Understand Docker container networks

* :doc:`network inspect <network_inspect>`
* :doc:`network create <network_create>`
* :doc:`network disconnect <network_disconnect>`
* :doc:`network ls <network_ls>`
* :doc:`network rm <network_rm>`
* :doc:`Docker コンテナ・ネットワークの理解 </engine/userguide/networking/dockernetworks>`

