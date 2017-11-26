# Blocking 阻塞





# Byte Order (Endians)

```c
uint16_t htons(uint16_t host_uint16);
//Returns host_uint16 converted to network byte order
uint32_t htonl(uint32_t host_uint32);
// Returns host_uint32 converted to network byte order
uint16_t ntohs(uint16_t net_uint16);
// Returns net_uint16 converted to host byte order
uint32_t ntohl(uint32_t net_uint32);
// Returns net_uint32 converted to host byte order
```