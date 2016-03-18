# asyncio_multicast
A simple wrapper for joining a multicast group using asyncio.
Usage:

    import socket
    import asyncio
    
    from asyncio_multicast.multicast import listen_multicast
    # The custom protocol written by the user
    from project import MulticastProtocol
    
    multicast_group_ip = '224.0.0.1' # ip of the multicast group to be joined
    host = '0.0.0.0'                 # ip of socket to which the socket has to be bound; default = '0.0.0.0'
    port = 14352                     # port of the socket to which the socket is to be bound; default = 0, i.e., random port
    loop = asyncio.get_event_loop()
    family = socket.AF_INET          # family of the socket; default = AF_INET
    # listen_multicast returns a coroutine which can be scheduled to run by passing it to asyncio.ensure_future()
    listen = listen_multicast(MulticastProtocol, multicast_group_ip, port, host, loop, family)
    asyncio.ensure_future(listen)
    try:
        loop.run_forever()
    except:
        loop.close()


