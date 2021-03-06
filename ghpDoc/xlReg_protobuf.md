<h1 class="libTop">xlReg protobuf spec</h1>

<pre><code>
package reg;

// All messages encoded with this protocol are subsequently encrypted using
// the server-provided AES session key and PKCS7-padded.

message XLRegMsg {
    enum Tag {
        RegCredRequest  = 1;
        RegCredReply    = 2;    // version, token (other registry credentials)

        Client      	= 3;    // token OR clientID, digSig
        ClientOK    	= 4;    // clientID, attrs

        // size means cluster size, constrained to 1 < n <= 64
        // epCount is number of menber endPoints, which must be 1 or 2
        Create      	= 5;    // clusterName, size, epCount
        CreateReply 	= 6;    // clusterID, size, epCount

        // Response to Join is clusterID + size + epCount -OR- error
        Join        	= 7;    // clusterName or clusterID
        JoinReply   	= 8;    // clusterID, attrs, size, epCount

        GetCluster  	= 9;    // clusterID, which = bit vector; -1 = all
        // Response to Get is a list of known members -OR- error
        ClusterMembers 	= 10;   // clusterID, which, tokens

        Bye         	= 11;   // from client
        Ack         	= 12;   // from server; followed by close

        Error       	= 13;   // errDesc; from server, followed by close

    }
    // the Token describes a member
    message Token {
        optional string Name        = 1;
	    optional uint64 Attrs       = 2;    // bit field
	    optional bytes  ID          = 3;    // 20 or 32 byte nodeID
        optional bytes  CommsKey    = 4;
        optional bytes  SigKey      = 5;
        // by convention, MyEnds[0] for inter-cluster comms,
        // MyEnds[1] for cluster-client comms
        // there must be epCount endPoints present
        repeated string MyEnds      = 6;    // overlay, endPoint
	    optional bytes  DigSig      = 7;    // over fields present, in order
	}
    optional Tag    Op              = 1;
    optional bytes  AesIV           = 2;
    optional bytes  AesKey          = 3;
    optional bytes  Salt1           = 4;    // error if len < 8
    optional bytes  Salt2           = 5;    // error if len < 8
    optional uint32 Version         = 6;    // little-endian, so stored D.C.B.A

    optional string ClientName      = 8;
    optional bytes  ClientID        = 9;
    optional uint64 ClientAttrs     = 10;
    optional Token  ClientSpecs     = 11;

    optional bytes  ClusterID       = 13;
    optional string ClusterName     = 14;
    optional uint32 ClusterSize     = 15;
    optional uint64 ClusterAttrs    = 16;
    optional uint32 EndPointCount   = 17;   // each member must have

    optional uint64 Which           = 20;   // bitset, members requested/sent
    repeated Token  Tokens          = 21;   // specs for members
    optional bytes  DigSig          = 22;

    optional string ErrDesc         = 23;

}
</code></pre>
