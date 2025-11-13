Plan:
    Motivation 
        Before IPv4 (1960 - 1980)
        Motivations for large-scale networking
        Alternative solutions at the time
        How IPv4 solved the problem
        Integration into pre-existing architectures
        Development of TCP/IP stack
    
    Implementation:
        The internet module
        Packet flow
        Packet format
        Adressing 
        Errors
    
    Limitations:
        The exhausion problem
    Proposed solutions:
        CIDR
        NAT

IPv4:
    Motivation:
        Before IPv4 (1960 - 1980):
            Networks were mostly small and isolated. 
            Examples include:
                ARPANET (1969): The first packet-switched network, funded by the U.S. Defense Advanced Research Projects Agency (DARPA). It connected a handful of research computers.
                Local area networks (LANs): Early Ethernet (1973–1976) and other local networks allowed computers in a single building to communicate.
                X.25 networks: Used by telecoms for packet-switched data, but these were centralized and not Internet-like.

            Addresses: Computers often used hostnames or machine-specific identifiers, not standardized numerical IPs. Communication was mostly via dedicated point-to-point links or very small packet-switched networks.
            
            Protocols: Early networks had their own protocols (NCP for ARPANET before TCP/IP, X.25 for telecom networks).
            State: There was no fully standardized stack. Researchers were experimenting with packet-switching, addressing, and routing in isolation. The notion of a modular, layered protocol stack was only beginning to crystallize.
            
        Motivations for large-scale networking:
            Interconnecting heterogeneous networks:
                By the late 1970s, there were many different networks (ARPANET, packet radio networks, satellite networks, and X.25-based public networks).
                Each had its own protocol; researchers realized they couldn’t easily communicate across networks.
                This “network of networks” problem was the main driver for a universal protocol.

            Scalability limits:
                Early ARPANET and LANs could only support a few dozen to a few hundred hosts efficiently.
                As more universities, labs, and government agencies joined, addressing and routing became unmanageable with network-specific schemes.

            Standardization of communication:
                Machines had different architectures (DEC PDP-11, IBM mainframes, etc.).
                Each had its own way of sending and interpreting data. A universal protocol allowed interoperable communication regardless of hardware or software.

            Research collaboration:
                Projects increasingly involved multiple institutions. Sharing computing resources, accessing remote files, or running remote programs became crucial.
                Without a common protocol, distributed computing across sites was impossible.

            Experimentation with new applications:
                Researchers wanted to test email, remote login, and file transfer across multiple sites.
                The lack of a consistent addressing and routing system limited these experiments to single networks.

        Alternative solutions at the time
            Before IPv4 (or TCP/IP), several ideas were explored:
                NCP (Network Control Protocol):
                    Used in ARPANET before TCP/IP.
                    Worked for small networks but could not scale well for multiple interconnected networks.
                    Lacked features like hierarchical addressing and flexible routing.

                X.25:
                    A standardized protocol for public packet-switched networks.
                    Very reliable, but centralized and slow, designed for telecom operators rather than research labs.
                    Difficult to extend to a global network of heterogeneous networks.

                CYCLADES network (France):
                    Pioneered the idea of end-to-end packet delivery, influencing TCP/IP design.
                    Showed that the network could be simpler and reliability could be handled at the host level, rather than the network.
                Other experimental internetworking protocols
                    Researchers proposed various hierarchical or gateway-based systems to connect networks, but none gained traction because:
                        They were often tied to specific technologies.
                        They lacked a clean, universal addressing scheme.

        IPv4 solved the networking problem incrementally, by providing a universal addressing and packet protocol that could overlay existing networks, rather than replacing them. Let’s break it down carefully.

        How IPv4 solved the problem
            The main problems at the time were:
                Networks had different hardware and protocols (e.g., ARPANET, packet radio, X.25).
                There was no universal addressing scheme, so you couldn’t route packets between networks.
                Existing protocols (like NCP) didn’t scale beyond a single network.

            IPv4 addressed these by:
                Standardized addressing
                    Every host got a 32-bit IP address.
                    The hierarchical structure (network ID + host ID) allowed routing across multiple networks.
                    Made it possible to assign addresses in a scalable, organized way.

                Packet format
                    IPv4 defined a universal header and rules for fragmentation, routing, and delivery.
                    Routers could read IPv4 packets regardless of the underlying physical network.

                Inter-network routing
                    IPv4 introduced logical networks on top of physical networks.
                    Gateways (later called routers) could connect multiple networks, forward packets based on IP addresses, and hide the differences of underlying link technologies.

                End-to-end principle
                    Reliability was handled by higher layers (TCP) rather than by the network itself.
                    This meant networks could be simple, and IPv4 could run on any underlying technology.

        Integration into pre-existing architectures
            IPv4 didn’t replace everything overnight; it was designed to overlay existing networks. Here’s how the transition worked:
            Gateway-based approach
                Existing networks stayed intact.
                Special machines called gateways connected networks.
                Gateways converted between local protocols and IPv4 packets.

            Dual-stack operation
                During transition, hosts could run both the old protocol (e.g., NCP) and IPv4.
                Gradually, as more networks adopted IPv4, legacy protocols could be retired.

            Incremental deployment
                IPv4 was first implemented on ARPANET and university research networks.
                Each new network could adopt IPv4 without disrupting existing local communication.
                Applications like email, remote login, and file transfer could start using IPv4 as soon as their hosts and gateways supported it.

            Standardized RFCs
                RFC 791 (IPv4) gave a complete specification of how packets should be formatted, addressed, routed, and handled.
                This made it easy for vendors and researchers to implement IPv4 consistently on diverse hardware

        Development of TCP/IP stack
            TCP/IP conception (1973–1978)
                Vinton Cerf and Robert Kahn designed TCP, which later split into TCP + IP.
                Goal: connect heterogeneous networks using a single internetworking protocol.
                IP handled addressing and routing; TCP handled reliability and end-to-end communication.

            IPv4 standardization (1981)
                RFC 791 defined IPv4.
                RFC 793 defined TCP.
                Together, these formed the TCP/IP stack: IP at the network layer, TCP at the transport layer.

            Layering model emerges
                By early 1980s, the four-layer “Internet model” (Application / Transport / Network / Link) was widely understood.
                Researchers still debated details, but TCP/IP defined a working, standardized stack for inter-network communication.

                 +------+ +-----+ +-----+     +-----+
                 |Telnet| | FTP | | TFTP| ... | ... |
                 +------+ +-----+ +-----+     +-----+
                       |   |         |           |
                      +-----+     +-----+     +-----+
                      | TCP |     | UDP | ... | ... |
                      +-----+     +-----+     +-----+
                         |           |           |
                      +--------------------------+----+
                      |    Internet Protocol & ICMP   |
                      +--------------------------+----+
                                     |
                        +---------------------------+
                        |   Local Network Protocol  |
                        +---------------------------+

                         Protocol Relationships

                               Figure 1.

        Transition and adoption
            1983: TCP/IP officially replaced NCP on ARPANET.
                This is often cited as the “birth of the Internet” in a practical sense.
            Mid-to-late 1980s: UNIX vendors, universities, and government labs adopted TCP/IP.
                Implementations varied slightly, but RFCs provided a standard reference.
            By the early 1990s: TCP/IP had become the de facto standard, powering the growing global Internet and replacing older proprietary protocols.

        Effect on networkings
            Allowed heterogeneous networks to interconnect and form the early Internet.
            Scaled to thousands of hosts at first, later millions.
            Standardized routing and addressing made applications portable across networks.
            Legacy protocols like NCP were eventually phased out.


        | Milestone                      | Year            |
        | ------------------------------ | --------------- |
        | TCP design begins              | 1973            |
        | Split TCP/IP, RFCs written     | 1978–1981       |
        | IPv4 + TCP RFCs                | 1981            |
        | TCP/IP required on ARPANET     | 1983            |
        | University & research adoption | 1983–late 1980s |
        | Global Internet standard       | early 1990s     |

    Implementation:
        The internet module:
            This protocol is called on by host-to-host protocols in an internet
            environment.  This protocol calls on local network protocols to carry
            the internet datagram to the next gateway or destination host.

            For example, a TCP module would call on the internet module to take a
            TCP segment (including the TCP header and user data) as the data
            portion of an internet datagram.  The TCP module would provide the
            addresses and other parameters in the internet header to the internet
            module as arguments of the call.  The internet module would then
            create an internet datagram and call on the local network interface to
            transmit the internet datagram.

        Packet flow

            The  model of operation for transmitting a datagram from one
            application program to another is illustrated by the following
            scenario:

                We suppose that this transmission will involve one intermediate
                gateway.

                The sending application program prepares its data and calls on its
                local internet module to send that data as a datagram and passes the
                destination address and other parameters as arguments of the call.

                The internet module prepares a datagram header and attaches the data
                to it.  The internet module determines a local network address for
                this internet address, in this case it is the address of a gateway.

            It sends this datagram and the local network address to the local
            network interface.

            The local network interface creates a local network header, and
            attaches the datagram to it, then sends the result via the local
            network.

            The datagram arrives at a gateway host wrapped in the local network
            header, the local network interface strips off this header, and
            turns the datagram over to the internet module.  The internet module
            determines from the internet address that the datagram is to be
            forwarded to another host in a second network.  The internet module
            determines a local net address for the destination host.  It calls
            on the local network interface for that network to send the
            datagram.

            This local network interface creates a local network header and
            attaches the datagram sending the result to the destination host.

            At this destination host the datagram is stripped of the local net
            header by the local network interface and handed to the internet
            module.

            The internet module determines that the datagram is for an
            application program in this host.  It passes the data to the
            application program in response to a system call, passing the source
            address and other parameters as results of the call.

                Application                                           Application
                Program                                                   Program
                        \                                                   /
                    Internet Module      Internet Module      Internet Module
                            \                 /       \                /
                            LNI-1          LNI-1      LNI-2         LNI-2
                                \           /             \          /
                            Local Network 1           Local Network 2



                                            Transmission Path

                                                Figure 2

            Gateways
                Gateways implement internet protocol to forward datagrams between
                networks.  Gateways also implement the Gateway to Gateway Protocol
                (GGP) [7] to coordinate routing and other internet control
                information.

                GPP
                    Gateway to Gateway Protocol, the protocol used primarily
                    between gateways to control routing and other gateway
                    functions.

                In a gateway the higher level protocols need not be implemented and
                the GGP functions are added to the IP module.


                                +-------------------------------+
                                | Internet Protocol & ICMP & GGP|
                                +-------------------------------+
                                        |                 |
                                +---------------+   +---------------+
                                |   Local Net   |   |   Local Net   |
                                +---------------+   +---------------+

                                        Gateway Protocols

                                            Figure 3.

        Packet format

            0                   1                   2                   3
            0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
            +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
            |Version|  IHL  |Type of Service|          Total Length         |
            +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
            |         Identification        |Flags|      Fragment Offset    |
            +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
            |  Time to Live |    Protocol   |         Header Checksum       |
            +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
            |                       Source Address                          |
            +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
            |                    Destination Address                        |
            +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
            |                    Options                    |    Padding    |
            +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

                                Example Internet Datagram Header

                                        Figure 4.

            Version:  4 bits
                The Version field indicates the format of the internet header.  This
                document describes version 4.

            IHL:  4 bits
                Internet Header Length is the length of the internet header in 32
                bit words.  Note that the minimum value for a correct header is 5.

            Type of Service:  8 bits
                The Type of Service provides an indication of the abstract
                parameters of the quality of service desired.  These parameters are
                to be used to guide the selection of the actual service parameters
                when transmitting a datagram through a particular network.  Several
                networks offer service precedence, which somehow treats high
                precedence traffic as more important than other traffic (generally
                by accepting only traffic above a certain precedence at time of high
                load).  The major choice is a three way tradeoff between low-delay,
                high-reliability, and high-throughput.

                Bits 0-2:  Precedence.
                Bit    3:  0 = Normal Delay,      1 = Low Delay.
                Bits   4:  0 = Normal Throughput, 1 = High Throughput.
                Bits   5:  0 = Normal Relibility, 1 = High Relibility.
                Bit  6-7:  Reserved for Future Use.

                    0     1     2     3     4     5     6     7
                +-----+-----+-----+-----+-----+-----+-----+-----+
                |                 |     |     |     |     |     |
                |   PRECEDENCE    |  D  |  T  |  R  |  0  |  0  |
                |                 |     |     |     |     |     |
                +-----+-----+-----+-----+-----+-----+-----+-----+

                    Precedence

                    111 - Network Control
                    110 - Internetwork Control
                    101 - CRITIC/ECP
                    100 - Flash Override
                    011 - Flash
                    010 - Immediate
                    001 - Priority
                    000 - Routine

                The use of the Delay, Throughput, and Reliability indications may
                increase the cost (in some sense) of the service.  In many networks
                better performance for one of these parameters is coupled with worse
                performance on another.  Except for very unusual cases at most two
                of these three indications should be set.

                The type of service is used to specify the treatment of the datagram
                during its transmission through the internet system.  Example
                mappings of the internet type of service to the actual service
                provided on networks such as AUTODIN II, ARPANET, SATNET, and PRNET
                is given in "Service Mappings" [8].

                The Network Control precedence designation is intended to be used
                within a network only.  The actual use and control of that
                designation is up to each network. The Internetwork Control
                designation is intended for use by gateway control originators only.
                If the actual use of these precedence designations is of concern to
                a particular network, it is the responsibility of that network to
                control the access to, and use of, those precedence designations.

            Total Length:  16 bits
                Total Length is the length of the datagram, measured in octets,
                including internet header and data.  This field allows the length of
                a datagram to be up to 65,535 octets.  Such long datagrams are
                impractical for most hosts and networks.  All hosts must be prepared
                to accept datagrams of up to 576 octets (whether they arrive whole
                or in fragments).  It is recommended that hosts only send datagrams
                larger than 576 octets if they have assurance that the destination
                is prepared to accept the larger datagrams.

                The number 576 is selected to allow a reasonable sized data block to
                be transmitted in addition to the required header information.  For
                example, this size allows a data block of 512 octets plus 64 header
                octets to fit in a datagram.  The maximal internet header is 60
                octets, and a typical internet header is 20 octets, allowing a
                margin for headers of higher level protocols.

            Identification:  16 bits
                An identifying value assigned by the sender to aid in assembling the
                fragments of a datagram.

            Flags:  3 bits
                Various Control Flags.

                Bit 0: reserved, must be zero
                Bit 1: (DF) 0 = May Fragment,  1 = Don't Fragment.
                Bit 2: (MF) 0 = Last Fragment, 1 = More Fragments.

                    0   1   2
                    +---+---+---+
                    |   | D | M |
                    | 0 | F | F |
                    +---+---+---+

            Fragment Offset:  13 bits
                This field indicates where in the datagram this fragment belongs.
                The fragment offset is measured in units of 8 octets (64 bits).  The
                first fragment has offset zero.

            Time to Live:  8 bits
                This field indicates the maximum time the datagram is allowed to
                remain in the internet system.  If this field contains the value
                zero, then the datagram must be destroyed.  This field is modified
                in internet header processing.  The time is measured in units of
                seconds, but since every module that processes a datagram must
                decrease the TTL by at least one even if it process the datagram in
                less than a second, the TTL must be thought of only as an upper
                bound on the time a datagram may exist.  The intention is to cause
                undeliverable datagrams to be discarded, and to bound the maximum
                datagram lifetime.

                The time to live is set by the sender to the maximum time the
                datagram is allowed to be in the internet system.  If the datagram
                is in the internet system longer than the time to live, then the
                datagram must be destroyed.

                This field must be decreased at each point that the internet header
                is processed to reflect the time spent processing the datagram.
                Even if no local information is available on the time actually
                spent, the field must be decremented by 1.  The time is measured in
                units of seconds (i.e. the value 1 means one second).  Thus, the
                maximum time to live is 255 seconds or 4.25 minutes.  Since every
                module that processes a datagram must decrease the TTL by at least
                one even if it process the datagram in less than a second, the TTL
                must be thought of only as an upper bound on the time a datagram may
                exist.  The intention is to cause undeliverable datagrams to be
                discarded, and to bound the maximum datagram lifetime.

            Protocol:  8 bits
                This field indicates the next level protocol used in the data
                portion of the internet datagram.  The values for various protocols
                are specified in "Assigned Numbers" [9].

            Header Checksum:  16 bits
                A checksum on the header only.  Since some header fields change
                (e.g., time to live), this is recomputed and verified at each point
                that the internet header is processed.

                The checksum algorithm is:
                    The checksum field is the 16 bit one's complement of the one's
                    complement sum of all 16 bit words in the header.  For purposes of
                    computing the checksum, the value of the checksum field is zero.

                This is a simple to compute checksum and experimental evidence
                indicates it is adequate, but it is provisional and may be replaced
                by a CRC procedure, depending on further experience.

                The internet header checksum is recomputed if the internet header is
                changed.  For example, a reduction of the time to live, additions or
                changes to internet options, or due to fragmentation.  This checksum
                at the internet level is intended to protect the internet header
                fields from transmission errors.

                There are some applications where a few data bit errors are
                acceptable while retransmission delays are not.  If the internet
                protocol enforced data correctness such applications could not be
                supported.

            Source Address:  32 bits
                The source address.  See section 3.2.

            Destination Address:  32 bits
                The destination address.  See section 3.2.

            Options
                The options may appear or not in datagrams.  They must be
                implemented by all IP modules (host and gateways).  What is optional
                is their transmission in any particular datagram, not their
                implementation.

                In some environments the security option may be required in all
                datagrams.

                The option field is variable in length.  There may be zero or more
                options.  There are two cases for the format of an option:

                Case 1:  A single octet of option-type.

                Case 2:  An option-type octet, an option-length octet, and the
                        actual option-data octets.

                The option-length octet counts the option-type octet and the
                option-length octet as well as the option-data octets.

                The option-type octet is viewed as having 3 fields:

                1 bit   copied flag,
                2 bits  option class,
                5 bits  option number.

                The copied flag indicates that this option is copied into all
                fragments on fragmentation.

                0 = not copied
                1 = copied

                The option classes are:

                0 = control
                1 = reserved for future use
                2 = debugging and measurement
                3 = reserved for future use

                The following internet options are defined:

                CLASS NUMBER LENGTH DESCRIPTION
                ----- ------ ------ -----------
                    0     0      -    End of Option list.  This option occupies only
                                    1 octet; it has no length octet.
                    0     1      -    No Operation.  This option occupies only 1
                                    octet; it has no length octet.
                    0     2     11    Security.  Used to carry Security,
                                    Compartmentation, User Group (TCC), and
                                    Handling Restriction Codes compatible with DOD
                                    requirements.
                    0     3     var.  Loose Source Routing.  Used to route the
                                    internet datagram based on information
                                    supplied by the source.
                    0     9     var.  Strict Source Routing.  Used to route the
                                    internet datagram based on information
                                    supplied by the source.
                    0     7     var.  Record Route.  Used to trace the route an
                                    internet datagram takes.
                    0     8      4    Stream ID.  Used to carry the stream
                                    identifier.
                    2     4     var.  Internet Timestamp.

                The options are optional in each datagram, but required in
                implementations.  That is, the presence or absence of an option is
                the choice of the sender, but each internet module must be able to
                parse every option.  There can be several options present in the
                option field.

                The options might not end on a 32-bit boundary.  The internet header
                must be filled out with octets of zeros.  The first of these would
                be interpreted as the end-of-options option, and the remainder as
                internet header padding.

                Every internet module must be able to act on every option.  The
                Security Option is required if classified, restricted, or
                compartmented traffic is to be passed.

            Padding:  variable
                The internet header padding is used to ensure that the internet
                header ends on a 32 bit boundary.  The padding is zero.

        Addressing

            To provide for flexibility in assigning address to networks and
            allow for the  large number of small to intermediate sized networks
            the interpretation of the address field is coded to specify a small
            number of networks with a large number of host, a moderate number of
            networks with a moderate number of hosts, and a large number of
            networks with a small number of hosts.  In addition there is an
            escape code for extended addressing mode.

            Address Formats:

            High Order Bits   Format                           Class
            ---------------   -------------------------------  -----
                    0            7 bits of net, 24 bits of host    a
                    10          14 bits of net, 16 bits of host    b
                    110         21 bits of net,  8 bits of host    c
                    111         escape to extended addressing mode

            A value of zero in the network field means this network.  This is
            only used in certain ICMP messages.  The extended addressing mode
            is undefined.  Both of these features are reserved for future use.

            The actual values assigned for network addresses is given in
            "Assigned Numbers" [9].

            The local address, assigned by the local network, must allow for a
            single physical host to act as several distinct internet hosts.
            That is, there must be a mapping between internet host addresses and
            network/host interfaces that allows several internet addresses to
            correspond to one interface.  It must also be allowed for a host to
            have several physical interfaces and to treat the datagrams from
            several of them as if they were all addressed to a single host.

            Address mappings between internet addresses and addresses for
            ARPANET, SATNET, PRNET, and other networks are described in "Address
            Mappings" [5].

        Errors
            Internet protocol errors may be reported via the ICMP messages [3].

        Interfaces:
            The functional description of user interfaces to the IP is, at best,
            fictional, since every operating system will have different
            facilities.  Consequently, we must warn readers that different IP
            implementations may have different user interfaces.  However, all IPs
            must provide a certain minimum  set of services to guarantee that all
            IP implementations can support the same protocol hierarchy.  This
            section specifies the functional interfaces required of all IP
            implementations.

            Internet protocol interfaces on one side to the local network and on
            the other side to either a higher level protocol or an application
            program.  In the following, the higher level protocol or application

            program (or even a gateway program) will be called the "user" since it
            is using the internet module.  Since internet protocol is a datagram
            protocol, there is minimal memory or state maintained between datagram
            transmissions, and each call on the internet protocol module by the
            user supplies all information necessary for the IP to perform the
            service requested.

            An Example Upper Level Interface

                The following two example calls satisfy the requirements for the user
                to internet protocol module communication ("=>" means returns):

                SEND (src, dst, prot, TOS, TTL, BufPTR, len, Id, DF, opt => result)

                    where:

                    src = source address
                    dst = destination address
                    prot = protocol
                    TOS = type of service
                    TTL = time to live
                    BufPTR = buffer pointer
                    len = length of buffer
                    Id  = Identifier
                    DF = Don't Fragment
                    opt = option data
                    result = response
                        OK = datagram sent ok
                        Error = error in arguments or local network error

                    Note that the precedence is included in the TOS and the
                    security/compartment is passed as an option.

                RECV (BufPTR, prot, => result, src, dst, TOS, len, opt)

                    where:

                    BufPTR = buffer pointer
                    prot = protocol
                    result = response
                        OK = datagram received ok
                        Error = error in arguments
                    len = length of buffer
                    src = source address
                    dst = destination address
                    TOS = type of service
                    opt = option data


            When the user sends a datagram, it executes the SEND call supplying
            all the arguments.  The internet protocol module, on receiving this
            call, checks the arguments and prepares and sends the message.  If the
            arguments are good and the datagram is accepted by the local network,
            the call returns successfully.  If either the arguments are bad, or
            the datagram is not accepted by the local network, the call returns
            unsuccessfully.  On unsuccessful returns, a reasonable report must be
            made as to the cause of the problem, but the details of such reports
            are up to individual implementations.

            When a datagram arrives at the internet protocol module from the local
            network, either there is a pending RECV call from the user addressed
            or there is not.  In the first case, the pending call is satisfied by
            passing the information from the datagram to the user.  In the second
            case, the user addressed is notified of a pending datagram.  If the
            user addressed does not exist, an ICMP error message is returned to
            the sender, and the data is discarded.

            The notification of a user may be via a pseudo interrupt or similar
            mechanism, as appropriate in the particular operating system
            environment of the implementation.

            A user's RECV call may then either be immediately satisfied by a
            pending datagram, or the call may be pending until a datagram arrives.

            The source address is included in the send call in case the sending
            host has several addresses (multiple physical connections or logical
            addresses).  The internet module must check to see that the source
            address is one of the legal address for this host.

            An implementation may also allow or require a call to the internet
            module to indicate interest in or reserve exclusive use of a class of
            datagrams (e.g., all those with a certain value in the protocol
            field).

            This section functionally characterizes a USER/IP interface.  The
            notation used is similar to most procedure of function calls in high
            level languages, but this usage is not meant to rule out trap type
            service calls (e.g., SVCs, UUOs, EMTs), or any other form of
            interprocess communication.

    Limitations:
        The exhausion problem:
            Problem, Goal, and Motivation
                As the Internet has evolved and grown over in recent years, it has
                become painfully evident that it is soon to face several serious
                scaling problems. These include:

                    1.   Exhaustion of the class-B network address space. One
                        fundamental cause of this problem is the lack of a network
                        class of a size which is appropriate for mid-sized
                        organization; class-C, with a maximum of 254 host
                        addresses, is too small while class-B, which allows up to
                        65534 addresses, is to large to be widely allocated.

                    2.   Growth of routing tables in Internet routers beyond the
                        ability of current software (and people) to effectively
                        manage.

                    3.   Eventual exhaustion of the 32-bit IP address space.
    
        add graphs from Geoff Huston — IPv4 Address Report

        Growth in routing table size?

    Attempts at a solutions:
        CIDR:
            This plan for allocating IP addresses should be undertaken as soon as
            possible.  We believe that this will suffice as a short term
            strategy, to fill the gap between now and the time when a viable long
            term plan can be put into place and deployed effectively.  This plan
            should be viable for at least three (3) years, after which time,
            deployment of a suitable long term solution is expected to occur.

            Classless Inter-Domain Routing (CIDR) is an IP addressing method introduced in 1993 (RFC 1519) to improve the efficiency of address allocation and routing in IPv4 networks.
            Instead of using the fixed class-based system (Class A, B, C), CIDR allows network prefixes of variable lengths — written as IP address/prefix length (for example, 192.168.0.0/20). This enables:
            More flexible subnetting — networks can be sized exactly to their needs.
            Address conservation — slows down IPv4 exhaustion by eliminating waste from large unused address blocks.
            Route aggregation (supernetting) — multiple contiguous networks can be represented as a single routing entry, reducing the size of global routing tables.

        NAT:
            The two most compelling problems facing the IP Internet are IP
            address depletion and scaling in routing. Long-term and short-term
            solutions to these problems are being developed. The short-term
            solution is CIDR (Classless InterDomain Routing) [2]. The long-term
            solutions consist of various proposals for new internet protocols
            with larger addresses.

            Until the long-term solutions are ready an easy way to hold down the
            demand for IP addresses is through address reuse. This solution takes
            advantage of the fact that a very small percentage of hosts in a stub
            domain are communicating outside of the domain at any given time. (A
            stub domain is a domain, such as a corporate network, that only
            handles traffic originated or destined to hosts in the domain).
            Indeed, many (if not most) hosts never communicate outside of their
            stub domain. Because of this, only a subset of the IP addresses
            inside a stub domain, need be translated into IP addresses that are
            globally unique when outside communications is required.

            This solution has the disadvantage of taking away the end-to-end
            significance of an IP address, and making up for it with increased
            state in the network. There are various work-arounds that minimize
            the potential pitfalls of this. Indeed, connection-oriented protocols
            are essentially doing address reuse at every hop.

            The huge advantage of this approach is that it can be installed
            incrementally, without changes to either hosts or routers. (A few
            unusual applications may require changes). As such, this solution can
            be implemented and experimented with quickly. If nothing else, this
            solution can serve to provide temporarily relief while other, more
            complex and far-reaching solutions are worked out.

                                       \ | /
                                     +---------------+
                                     |Regional Router|
                                     +---------------+
                                   WAN |           | WAN
                                       |           |
                   Stub A .............|....   ....|............ Stub B
                                       |           |
                     {s=198.76.29.7,^  |           |  v{s=198.76.29.7,
                      d=198.76.28.4}^  |           |  v d=198.76.28.4}
                       +-----------------+       +-----------------+
                       |Stub Router w/NAT|       |Stub Router w/NAT|
                       +-----------------+       +-----------------+
                             |                         |
                             |  LAN               LAN  |
                       -------------             -------------
                                 |                 |
               {s=10.33.96.5, ^  |                 |  v{s=198.76.29.7,
                d=198.76.28.4}^ +--+             +--+ v d=10.81.13.22}
                                |--|             |--|
                               /____\           /____\
                             10.33.96.5       10.81.13.22

                     Figure 2: Basic NAT Operation

        Conclusions
            NAT may be a good short term solution to the address depletion and
            scaling problems. This is because it requires very few changes and
            can be installed incrementally. NAT has several negative
            characteristics that make it inappropriate as a long term solution,
            and may make it inappropriate even as a short term solution. Only
            implementation and experimentation will determine its
            appropriateness.

            The negative characteristics are:
                1. It requires a sparse end-to-end traffic matrix. Otherwise, the NAT
                tables will be large, thus giving lower performance. While the
                expectation is that end-to-end traffic matrices are indeed sparse,
                experience with NAT will determine whether or not they are. In any
                event, future applications may require a rich traffic matrix (for
                instance, distributed resource discovery), thus making long-term use
                of NAT unattractive.

                2. It increases the probability of mis-addressing.

                3. It breaks certain applications (or at least makes them more difficult
                to run).

                4. It hides the identity of hosts. While this has the benefit of
                privacy, it is generally a negative effect.

                5. Problems with SNMP, DNS, ... you name it.

