# Packet frame format:
* fixed header
* variable header
* payload

1. Fixed header:
    * First byte:
        * first 4 bits are reserved & used for special usage, with publishing
        * last 4 bits are control bits, with 14 control messages to use

> MQTT can support up to 268 MB in one message

2. Variable header:
    * anything that might appear in a packet and appear not in another
___
# Messages:
1. CONNECT:
    * fixed header = 0x10
    * variable header, is postponed until before sending

`Frame`
|<type>|<unknown_at_start>|'M'|'Q'|'T'|'T'| 4 |<flags>|<keep_alive_MSB>|<keep_alive_LSB>|<user_name>|<password>|
|:-:   |:-:               |:-:|:-:|:-:|:-:|:-:|:-:    |:-:             |:-:             |:-:        |:-:       |
|1     |<x>               | 1 | 1 | 1 | 1 | 1 |1      |1               |1               |<variable> |<variable>|

> keepAlive flag: determines the time the server should ping the client to ensure connection

2. CONNACK:
    * fixed header = 0x10
    * variable header, has the length which is 4 byte

`Frame`
|<type>|<length>|<reserved>|<ack_msg>|
|:-:   |:-:     |:-:       |:-:      |
|1     |1       |1         |1        |

3. PUBLISH:
    * it is the only message that supports Quality of Service (QoS)
    
`Frame`
|<type>|<unknown_at_start>|...|<topic_id>|
|:-:   |:-:               |:-:|:-:       |
|      |                  |   |          |

4. PUBACK:
    * check only the message type

5. SUBSCRIBE

6. SUBACK:
    * check only the message type
    
