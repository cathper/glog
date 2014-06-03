Docker registry via SSH
=======================

I just spend an hour on figuring out how to run my own private registry. Well,
that I did several months ago, but I wanted to get it secured; by default the
registry is open to the world.

On my server I have ``docker run --rm -p 127.0.0.1:5000:5000 registry``.

On my laptop I have the following two running:

.. code-block:: shell

    $ sudo ncat -k -l -p 80 -c 'nc localhost 5000'

    $ ssh -N -L 5000:127.0.0.1:5000 <server>

The first is because docker wants the registry to listen on port 80, so I just
port forward 80 to 5000 on my laptop. The second makes ssh port forward port
5000 on localhost to port 5000 on my server.

Then I have

.. code-block:: shell

    $ echo "127.0.0.1 registry.spag.dk" | sudo tee -a /etc/hosts
    $ docker tag scratch registry.spag.dk/scratch
    $ docker push registry.spag.dk/scratch

I think this is more light-weight than SSL, login etc.
