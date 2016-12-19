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

**HTTP Status Code**: `301  Moved Permanently`

**JSON Response**: N/A

**Comment**: Redirects to the `README.md` file of `pilad` package in Github, using the version executed. If version does not exist in Github, it uses master.

---

**Description**: Show status.

**HTTP Method**: `GET`

**HTTP Endpoint**: `/_status`
 
**Scenario**: N/A

**HTTP Status Code**: `200 OK`

**JSON Response**:
  * `status`: Status of piladb, e.g. `OK`.
  * `version`: Version of piladb. If not set, uses `master`.
  * `host`: OS and architecture of host machine, e.g. `linux_amd64`
  * `pid`: Process ID.
  * `started_at`: Date `pilad` was started (RFC3339).
  * `running_for`: Time server was running in seconds.
  * `number_goroutines`: Number of goroutines started used by the server.
  * `memory_alloc`: data allocated in memory, in KiB, MiB or GiB.

**Comment**: N/A

---

---

## Config

---

**Description**: Show configuration keys and values.

**HTTP Method**: `GET`

**HTTP Endpoint**: `/_config`
 
**Scenario**: N/A

**HTTP Status Code**: `200 OK`

**JSON Response**:
  * `stacks`: A collection containing configuration keys and values.
  
**Comment**: N/A

---

**Description**: Show configuration keys and values with serialization errors.

**HTTP Method**: `GET`

**HTTP Endpoint**: `/_config`
 
**Scenario**: Response can't be serialized.  

**HTTP Status Code**: `400 Bad Request`

**JSON Response**: N/A

**Comment**: N/A

---

**Description**: Set a configuration value.

**HTTP Method**: `POST`

**HTTP Endpoint**: `/_config/$CONFIG_KEY`

**Request Payload**: `{"element":"$CONFIG_VALUE"}`
 
**Scenario**: N/A  

**HTTP Status Code**: `200 OK`

**JSON Response**:
  * `element`: `$CONFIG_VALUE` set to `$CONFIG_KEY`

**Comment**: `$CONFIG_KEY` must exist.

---

**Description**: Set a configuration value to a non-existing key.

**HTTP Method**: `POST`

**HTTP Endpoint**: `/_config/$CONFIG_KEY`

**Request Payload**: `{"element":"$CONFIG_VALUE"}`
 
**Scenario**: `$CONFIG_KEY` does not exist.

**HTTP Status Code**: `410 Gone`

**JSON Response**: N/A

**Comment**: N/A

---

**Description**: Set a configuration value without providing value.

**HTTP Method**: `POST`

**HTTP Endpoint**: `/_config/$CONFIG_KEY`

**Request Payload**: N/A
 
**Scenario**: `$CONFIG_VALUE` is not provided in Request Payload.

**HTTP Status Code**: `400 Bad Request`

**JSON Response**: N/A

**Comment**: N/A

---

**Description**: Set a configuration value with serialization errors.

**HTTP Method**: `POST`

**HTTP Endpoint**: `/_config/$CONFIG_KEY`

**Request Payload**: N/A
 
**Scenario**: Response cannot be serialized.

**HTTP Status Code**: `400 Bad Request`

**JSON Response**: N/A

**Comment**: N/A

---



















# Sample

**Description**:

**HTTP Method**:

**HTTP Endpoint**:
 
**Scenario**:

**HTTP Status Code**:

**JSON Response**:
