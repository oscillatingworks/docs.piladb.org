# Specification

This page represents the technical specification of **piladb** functionality. In other words, this is a contract between the server and clients, which states what the former must response on latter's requests.

It contains all available operations that a client can execute, its requiremnts and 
a description of the expected content to return by the server.

## Main

---

**Description**: Show API documentation.

**HTTP Method**: `GET`

**HTTP Endpoint**: `/`
 
**Scenario**: N/A

**HTTP Status Code**: `301`

**JSON Response**: N/A

**Comment**: Redirects to the `README.md` file of `pilad` package in Github, using the version executed. If version does not exist in Github, it uses master.

---

**Description**: Show status.

**HTTP Method**: `GET`

**HTTP Endpoint**: `/_status`
 
**Scenario**: N/A

**HTTP Status Code**: `200`

**JSON Response**:
  * `status`: Status of piladb, e.g. `OK`.
  * `version`: Version of piladb. If not set, uses `master`.
  * `host`: OS and architecture of host machine, e.g. `linux_amd64`
  * `pid`: Process ID.
  * `started_at`: Date `pilad` was started (RFC3339).
  * `running_for`: Time server was running in seconds.
  * `number_goroutines`: Number of goroutines started used by the server.
  * `memory_alloc`: data allocated in memory, in KiB, MiB y GiB.

**Comment**: N/A

---

---

## Config

---

**Description**: 

**HTTP Method**:

**HTTP Endpoint**:
 
**Scenario**:

**HTTP Status Code**:

**JSON Response**:

---

# Sample

**Description**:

**HTTP Method**:

**HTTP Endpoint**:
 
**Scenario**:

**HTTP Status Code**:

**JSON Response**:
