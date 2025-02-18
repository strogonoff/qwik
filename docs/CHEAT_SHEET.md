# Cheat sheet

## Special HTML attributes

HTML attributes with the following syntax have a special meaning to Qwik.

1. They always contain `:` characters to make them less likely to collide with existing attributes.
2. The consist of a "key" and a "value", separated by `=`, as described in the following tables.

### General

| Syntax              | Meaning                                                                                                                 |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| `:`                 | Marker which signifies that the element has injector                                                                    |
| `on:<name>="<QRL>"` | If the event `name` is detected then the handler defined by the `QRL` loaded and executed. See [QRL](#qrl) table below. |
| `bind:<key>="attr"` | Bind the `attr` to the service identified by `key`. See the [bindings note](#bindings)                                  |
| `::name=QRL`        | Entity with key `name` is defined at `QRL`.                                                                             |
| `key:=JSON`         | State of the `Entity` identified by `key`, serialized into JSON.                                                        |
| `:.=JSON`           | Component state, serialized into JSON.                                                                                  |

### JSX Components

| Syntax                               | Meaning                                                                           |
| ------------------------------------ | --------------------------------------------------------------------------------- |
| `q:view=QRL`                         | Component render `QRL`, which points to the component's template render function. |
| `q:entity=[Service1, Service2, ...]` | Entities to be provided by this element's injector.                               |
| `$<prop>={key}`                      | Associate Component `prop` with service identified by `key`.                      |

### Special events

| Syntax                 | Meaning                            |
| ---------------------- | ---------------------------------- |
| `on:qInit="<QRL>"`     | Fired when the DOM is first loaded |
| `on:qInterval="<QRL>"` | TODO: document                     |
| `on:qTimeout="<QRL>"`  | TODO: document                     |
| `on:qRender="<QRL>"`   | TODO: document                     |

### Binding syntax

NOTE: The key/value pair is reversed in the binding, so that it is easy to query for all of the data bindings by `key`.

## QRL

| Syntax                 | Meaning                                                                                                                                           |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `./path`               | Import code from URL and run `default` handler <div> `(await import('./path.js')).default.call(injector) `</div>                                  |
| `key:/path`            | Import code from protocol mapped URL and run `default` handler <div> `(await import(CONFIG.protocol[key] + '/path.js')).default(injector) `</div> |
| `./path#foo`           | Import code from URL and run `foo` handler <div> `(await import('./path.js')).foo(injector) `</div>                                               |
| `./path#foo?key=value` | Import code from URL and run `foo` handler with params <div> `(await import('./path.js')).foo(injector) `</div>                                   |
| `./path#?key=value`    | Import code from URL and run `default` handler with params <div> `(await import('./path.js')).default(injector) `</div>                           |
