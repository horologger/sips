### Given john@doe and nothing else, how do we determine if it's valid and if so return associated meta-data?

# Don't consider caching for now.

# First check fabric provided data.

# Is there a record for john@doe then return the data. (Zone signed by john@doe owner)
# If not, check @doe and look for a record for john. TXT?
# If found, return the data.
# If @doe has an API endpoint record, then call the API endpoint and return the data.
# Get john@doe's certificate and verify.

## Check order
# Fabric john@doe
# Fabric @doe
# Operator API @doe
# Data john@doe ?? how to get this?  From Operator API?
# Data @doe 



# cat smith.zone 
@smith. 3600 CLASS2 A 99.222.149.207
@smith. 3600 CLASS2 TXT "~01~~99.222.149.207/@smith/"
@smith. 3600 CLASS2 TXT "~09~~smith Cognitive Effects"
@smith. 3600 CLASS2 TXT "~01~adam~https://smith.com"
@smith. 3600 CLASS2 TXT "~01~bart~99.222.149.207/bart@smith/"
@smith. 3600 CLASS2 TXT "~02~adam~040e739ce127b6d77c34ea12e10245b72742a26c67ce0575c3b0add38dc297b4282"
@smith. 3600 CLASS2 TXT "~03~adam~wss://relay@primal,wss://relay.primal.net,ws://194.195.222.47:4848/"

# cat adam@smith.zone 
adam@smith. 3600 CLASS2 A 99.222.149.207
adam@smith. 3600 CLASS2 TXT "~01~~99.222.149.207/@smith/adam/"
adam@smith. 3600 CLASS2 TXT "~09~~adam Smith The Person"
adam@smith. 3600 CLASS2 TXT "~01~santa.~https://thenorthpole.com" #santa.adam@smith
adam@smith. 3600 CLASS2 TXT "~02~~040e739ce127b6d77c34ea12e10245b72742a26c67ce0575c3b0add38dc297b4282"
adam@smith. 3600 CLASS2 TXT "~03~~wss://relay@primal,wss://relay.primal.net,ws://194.195.222.47:4848/"



```javascript

// Parse the handle into subname and top-level space
let (subname, space) = handle.split('@');

// Check if the space is a valid space using space-cli getspace
space-cli getspace '@'+space

// If the result is null, then the space is not valid
if (result === null) {
    return null;
}

// Otherwise, parse out the covenant.data as a hex string

// Process the hex string per SIPXX

// The first byte is the version byte

// If the version is not 0x01, return null
if (version !== 0x01) {
    return null;
}

// While there is more bytes to process
    // Get the next byte as the type and following length byte
    // Get the value as the next length bytes of data
    // Switch on the type and process the value accordingly
    // If the type is not recognized, return null
    // If the value is valid, interpret the value accordingly
    // Case type of:
        // 0x00 | Owner URI | RPC Interface | `http://192.168.1.254:8080/v1/services/getspace` |
        // 0x01 | Owner Web | Info Website | `https://spacesops.com` |
        //0x02 | Nostr Pubkey | 64 hex digits (32 bytes) | `040e739ce127b6d77c34ea12e10245b72742a26c67ce0575c3b0add38dc297b4282` |
        //0x03 | Nostr Relay | WebSocket relay (IP, DNS, Spaces) | `wss://relay@primal,wss://relay.primal.net,ws://194.195.222.47:4848/` |

// Prior to proof commitment, only the space operator knows if a subname is valid or not.

// If an operator gets a request for a handle for a space it doesn't control, does it act as a proxy and forward the request to the space operator?  Can it cache results?  If so for how long?

// If information is not found in the "data", then try the fabric node net for data.
//  Can a subspace owner create/sign/publish zones just for john@doe?
// If all this fails then return null.

// If the hex string is not valid, return null
return null;

```