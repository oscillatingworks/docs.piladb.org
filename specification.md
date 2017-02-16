# Specification

This page represents the technical specification of **piladb** functionality. In other words, this is a contract between the server and clients, which states what the former must response on latter's requests.

It contains all available operations that a client can execute, its requirements and  
a description of the expected content to return by the server.

Changes in the specification are expected to happen in new releases, and they will be correctly documented.

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
* `started_at`: Date `pilad` was started in local time \(RFC3339\).
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

**Description**: Show a configuration value.

**HTTP Method**: `GET`

**HTTP Endpoint**: `/_config/$CONFIG_KEY`

**Scenario**: N/A

**HTTP Status Code**: `200 OK`

**JSON Response**:

* `element`: Value of `$CONFIG_KEY`.

**Comment**: N/A

---

**Description**: Show configuration value from a non-existing key.

**HTTP Method**: `GET`

**HTTP Endpoint**: `/_config/$CONFIG_KEY`

**Scenario**: `$CONFIG_KEY` does not exist.

**HTTP Status Code**: `410 Gone`

**JSON Response**: N/A

**Comment**: N/A

---

**Description**: Show configuration value with serialization errors.

**HTTP Method**: `GET`

**HTTP Endpoint**: `/_config/$CONFIG_KEY`

**Scenario**: Response cannot be serialized.

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

* `element`: `$CONFIG_VALUE` set to `$CONFIG_KEY`.

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

**Request Payload**: `{"element":"$CONFIG_VALUE"}`

**Scenario**: Response cannot be serialized.

**HTTP Status Code**: `400 Bad Request`

**JSON Response**: N/A

**Comment**: `$CONFIG_VALUE` is not JSON-compatible.

---

---

## Databases

---

**Description**: Show databases.

**HTTP Method**: `GET`

**HTTP Endpoint**: `/databases`

**Scenario**: N/A

**HTTP Status Code**: `200 OK`

**JSON Response**:

* `number_of_databases`: Number of Databases.
* `databases`: Array with databases information.
  * `number_of_stacks`: Number of stacks associated to the database.
  * `name`: Name of the database.
  * `id`: UUID of the database.

**Comment**: N/A

---

**Description**: Show a database.

**HTTP Method**: `GET`

**HTTP Endpoint**: `/databases/$DATABASE_ID`

**Scenario**: N/A

**HTTP Status Code**: `200 OK`

**JSON Response**:

* `number_of_stacks`: Number of stacks associated to the database.
* `name`: Name of the database.
* `id`: UUID of the database.

**Comment**: `$DATABASE_ID` can be either the ID or the name of the database.

---

**Description**: Show a database that does not exist.

**HTTP Method**: `GET`

**HTTP Endpoint**: `/databases/$DATABASE_ID`

**Scenario**: `$DATABASE_ID` does not exist.

**HTTP Status Code**: `410 Gone`

**JSON Response**: N/A

**Comment**: ID nor name of the database do not exist.

---

**Description**: Create a database.

**HTTP Method**: `PUT`

**HTTP Endpoint**: `/databases?name=$DATABASE_NAME`

**Scenario**: N/A

**HTTP Status Code**: `201 Created`

**JSON Response**:

* `number_of_stacks`: Number of stacks associated to the database. Must be `0`.
* `name`: Name of the database.
* `id`: UUID of the database, generated from the name of the database.

**Comment**: N/A

---

**Description**: Create a database without providing the name.

**HTTP Method**: `PUT`

**HTTP Endpoint**: `/databases`

**Scenario**: `name` is not provided in the query string.

**HTTP Status Code**: `400 Bad Request`

**JSON Response**: N/A

**Comment**: N/A

---

**Description**: Delete a database.

**HTTP Method**: `DELETE`

**HTTP Endpoint**: `/databases/$DATABASE_ID`

**Scenario**: N/A

**HTTP Status Code**: `204 No Content`

**JSON Response**: N/A

**Comment**: `$DATABASE_ID` can be either the ID or the name of the database.

---

---

## Stacks

---

**Description**: Show stacks of a database.

**HTTP Method**: `GET`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks`

**Scenario**: N/A

**HTTP Status Code**: `200 OK`

**JSON Response**:

* `stacks`: Array containing all stacks information.
  * `id`: UUID of the stack.
  * `name`: Name of the stack.
  * `peek`: Element on top of the stack.
  * `size`: Number of elements contained in the stack.
  * `created_at`: Creation date of the stack in local time \(RFC3339\).
  * `updated_at`: Date the stack was updated for the last time in local time \(RFC3339\).
  * `read_at`: Date the stack was read or accessed for the last time in local time \(RFC3339\).

**Comment**: This doesn't update `read_at` value.

---

**Description**: Show stacks of a database in key-value format.

**HTTP Method**: `GET`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks?kv`

**Scenario**: N/A

**HTTP Status Code**: `200 OK`

**JSON Response**:

* `stacks`: Set of key-value's:
  * Key: name of the stack — Value: peek of the stack.

**Comment**: N/A

---

**Description**: Show stacks of a non-existent database.

**HTTP Method**: `GET`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks`

**Scenario**: `$DATABASE_ID` does not exist as a name of ID of a database.

**HTTP Status Code**: `410 Gone`

**JSON Response**: N/A

**Comment**: Also applies when `kv` is provided.

---

**Description**: Show stacks with serialization errors.

**HTTP Method**: `GET`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks`

**Scenario**: Response cannot be serialized.

**HTTP Status Code**: `400 Bad Request`

**JSON Response**: N/A

**Comment**: Also applies when `kv` is provided.

---

**Description**: Create a stack from a database.

**HTTP Method**: `PUT`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks?name=$STACK_NAME`

**Scenario**: N/A

**HTTP Status Code**: `201 Created`

**JSON Response**:

* `id`: UUID of the stack generated from the name of the database and `$STACK_NAME`.
* `name`: Name of the stack. Must be `$STACK_NAME`.
* `peek`: Element on top of the stack. Must be `null`.
* `size`: Number of elements contained in the stack. Must be 0.
* `created_at`: Creation date of the stack in local time \(RFC3339\).
* `updated_at`: Date the stack was updated for the last time in local time \(RFC3339\).
* `read_at`: Date the stack was read or accessed for the last time in local time \(RFC3339\).

**Comment**:

* `created_at`, `updates_at` and `read_at` must be similar.
* `$DATABASE_ID` can be either the ID or the name of the database.

---

**Description**: Create a stack from a non-existing database.

**HTTP Method**: `PUT`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks?name=$DATABASE_NAME`

**Scenario**: `$DATABASE_ID` does not exist.

**HTTP Status Code**: `410 Gone`

**JSON Response**: N/A

**Comment**: N/A

---

**Description**: Create a stack without providing the name.

**HTTP Method**: `PUT`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks`

**Scenario**: `name` is not provided in the query string.

**HTTP Status Code**: `400 Bad Request`

**JSON Response**: N/A

**Comment**: N/A

---

**Description**: Create a stack that already exists.

**HTTP Method**: `PUT`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks`

**Scenario**: `name` is not provided in the query string.

**HTTP Status Code**: `409 Conflict`

**JSON Response**: N/A

**Comment**: N/A

---

**Description**: Show a stack.

**HTTP Method**: `GET`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks/$STACK_ID`

**Scenario**: N/A

**HTTP Status Code**: `200 OK`

**JSON Response**:

* `id`: UUID of the stack.
* `name`: Name of the stack.
* `peek`: Element on top of the stack.
* `size`: Number of elements contained in the stack.
* `created_at`: Creation date of the stack in local time \(RFC3339\).
* `updated_at`: Date the stack was updated for the last time in local time \(RFC3339\).
* `read_at`: Date the stack was read or accessed for the last time in local time \(RFC3339\).

**Comment**:

* `read_at` value gets updated.
* `$DATABASE_ID` can be either the ID or the name of the database.
* `$STACK_ID` can be either the ID or the name of the stack.

---

**Description**: `PEEK` operation on a stack.

**HTTP Method**: `GET`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks/$STACK_ID?peek`

**Scenario**: N/A

**HTTP Status Code**: `200 OK`

**JSON Response**:

* `element`: Element on top of the stack.

**Comment**:

* `read_at` value gets updated.
* `$DATABASE_ID` can be either the ID or the name of the database.
* `$STACK_ID` can be either the ID or the name of the stack.

---

**Description**: `SIZE` operation on a stack.

**HTTP Method**: `GET`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks/$STACK_ID?size`

**Scenario**: N/A

**HTTP Status Code**: `200 OK`

**JSON Response**:

* Size of the stack as number.

**Comment**:

* `read_at` value gets updated.
* `$DATABASE_ID` can be either the ID or the name of the database.
* `$STACK_ID` can be either the ID or the name of the stack.

---

**Description**: Show a stack where database or stack do not exist.

**HTTP Method**: `GET`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks/$STACK_ID`

**Scenario**: `$DATABASE_ID` or `$STACK_ID` do not exist.

**HTTP Status Code**: `410 Gone`

**JSON Response**: N/A

**Comment**: Also applies when `peek` or `size` are provided.

---

**Description**: `PUSH` operation on a stack.

**HTTP Method**: `POST`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks/$STACK_ID`

**Request Payload**: `{"element":"$ELEMENT_VALUE"}`

**Scenario**: N/A

**HTTP Status Code**: `200 OK`

**JSON Response**:

* `element`: Pushed element value. Must be `$ELEMENT_VALUE`.

**Comment**:

* `updated_at` and `read_at` value get updated.
* `$ELEMENT_VALUE` is JSON-compatible.
* `$DATABASE_ID` can be either the ID or the name of the database.
* `$STACK_ID` can be either the ID or the name of the stack.

---

**Description**: `PUSH` operation on a full stack.

**HTTP Method**: `POST`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks/$STACK_ID`

**Request Payload**: `{"element":"$ELEMENT_VALUE"}`

**Scenario**: Config `MAX_STACK_SIZE` value is reached, stack cannot contain more elements.

**HTTP Status Code**: `406 Not Acceptable`

**JSON Response**: N/A

**Comment**: N/A

---

**Description**: `PUSH` operation on a stack where database or stack do not exist.

**HTTP Method**: `POST`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks/$STACK_ID`

**Request Payload**: N/A

**Scenario**: `$DATABASE_ID` or `$STACK_ID` do not exist.

**HTTP Status Code**: `410 Gone`

**JSON Response**: N/A

**Comment**: N/A

---

**Description**: `PUSH` operation on a stack with serializing errors.

**HTTP Method**: `POST`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks/$STACK_ID`

**Request Payload**: `{"element":"$ELEMENT_VALUE"}`

**Scenario**: `$ELEMENT_VALUE` cannot be serialized.

**HTTP Status Code**: `400 Bad Request`

**JSON Response**: N/A

**Comment**: N/A

---

**Description**: `POP` operation on a stack.

**HTTP Method**: `DELETE`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks/$STACK_ID`

**Scenario**: Stack is not empty.

**HTTP Status Code**: `200 OK`

**JSON Response**:

* `element`: Popped element value. Must be `$ELEMENT_VALUE`.

**Comment**:

* `updated_at` and `read_at` value get updated.
* `size` value decrements in one.
* `$DATABASE_ID` can be either the ID or the name of the database.
* `$STACK_ID` can be either the ID or the name of the stack.

---

**Description**: `POP` operation on an empty stack.

**HTTP Method**: `DELETE`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks/$STACK_ID`

**Scenario**: Stack is empty.

**HTTP Status Code**: `204 No Content`

**JSON Response**: N/A

**Comment**: N/A

---

**Description**: `FLUSH` operation on a stack.

**HTTP Method**: `DELETE`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks/$STACK_ID?flush`

**Scenario**: N/A

**HTTP Status Code**: `200 OK`

**JSON Response**:

* `id`: UUID of the stack.
* `name`: Name of the stack.
* `peek`: Element on top of the stack. Must be 0.
* `size`: Number of elements contained in the stack. Must be 0.
* `created_at`: Creation date of the stack in local time \(RFC3339\).
* `updated_at`: Date the stack was updated for the last time in local time \(RFC3339\).
* `read_at`: Date the stack was read or accessed for the last time in local time \(RFC3339\).

**Comment**:

* `updated_at` and `read_at` value get updated.
* `$DATABASE_ID` can be either the ID or the name of the database.
* `$STACK_ID` can be either the ID or the name of the stack.

---

**Description**: Delete stack.

**HTTP Method**: `DELETE`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks/$STACK_ID?full`

**Scenario**: N/A

**HTTP Status Code**: `204 No Content`

**JSON Response**: N/A

**Comment**:

* `$DATABASE_ID` can be either the ID or the name of the database.
* `$STACK_ID` can be either the ID or the name of the stack.

---

**Description**: `POP` operation on a stack where database or stack do not exist.

**HTTP Method**: `DELETE`

**HTTP Endpoint**: `/databases/$DATABASE_ID/stacks/$STACK_ID`

**Scenario**: `$DATABASE_ID` or `$STACK_ID` do not exist.

**HTTP Status Code**: `410 Gone`

**JSON Response**: N/A

**Comment**: Also applies when `peek` or `full` are provided.

---

---



