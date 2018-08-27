# Using a Messenger

When you need to perform IPC, using a Messenger for your interface is simpler than using AIDL, 
because Messenger queues all calls to the service. A pure AIDL interface sends simultaneous 
requests to the service, which must then handle multi-threading.

For most applications, the service doesn't need to perform multi-threading, so using a Messenger allows 
the service to handle one call at a time. If it's important that your service be multi-threaded, 
use AIDL to define your interface.


# Here's a summary of how to use a Messenger

# 1.  The service implements a Handler that receives a callback for each call from a client.
2.  The service uses the Handler to create a Messenger object (which is a reference to the Handler).
3.  The Messenger creates an IBinder that the service returns to clients from onBind().
4.  Clients use the IBinder to instantiate the Messenger (that references the service's Handler), 
    which the client uses to send Message objects to the service.
5.  The service receives each Message in its Handler—specifically, in the handleMessage() method.


In this way, there are no methods for the client to call on the service. Instead, 
the client delivers messages (Message objects) that the service receives in its Handler.
