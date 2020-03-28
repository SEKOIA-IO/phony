
# phony

  Tiny command line program that accepts a template and outputs fake data.

  ![](https://cldup.com/RZoAhReDqN.gif)

## Examples

```bash
# publish email to nsq every 1ms.
echo '{"email":"{{email}}", "subject": "welcome!"}' \
  | phony --tick 1ms \
  | json-to-nsq --topic users

# add users to FoundationDB.
echo "'set {{username}} {{avatar}}'" \
  | phony \
  | xargs -L1 -n3 fdbcli --exec

# add users to MongoDB.
echo "'db.users.insert({ name: \"{{name}}\" })'" \
  | phony \
  | xargs -L1 -n1 mongo --eval

# add users to Redis.
echo "set {{username}} {{avatar}}" \
  | phony \
  | xargs -L1 -n3 redis-cli

# send a single request using curl.
echo 'country={{country}}' \
  | phony --max 1 \
  | curl -d @- httpbin.org/post
```

## Installation

```bash
$ go get github.com/yields/phony
```

## Usage

```text

Usage: phony
  [--tick d]
  [--max n]
  [--list]

  phony -h | --help
  phony -v | --version

Options:
  --list          list all available generators
  --max n         generate data up to n [default: -1]
  --tick d        generate data every d [default: 10ms]
  -v, --version   show version information
  -h, --help      show help information

```

## Generators

### Avatar

Generate an uri to an avatar picture

```bash
$ echo "{{avatar}}" | phony --max 1
https://s3.amazonaws.com/uifaces/faces/twitter/areus/128.jpg
```

### Color

Generate a textual name of a color

```bash
$ echo "{{color}}" | phony --max 1
red
```

### Country

Generate the name of a country

```bash
$ echo "{{country}}" | phony --max 1
Argentina
```

### Country code

Generate the short alphabetic geographical code of a country

```bash
$ echo "{{country.code}}" | phony --max 1
AR
```

### Domain

Generate a domain

```bash
$ echo "{{domain}}" | phony --max 1
example.com
```

### Domain name

Generate a domain name

```bash
$ echo "{{domain.name}}" | phony --max 1
example
```

### Domain TLD

Generate a domain TLD

```bash
$ echo "{{domain.name}}" | phony --max 1
org
```

### Double

Generate a double number

```bash
$ echo "{{double}}" | phony --max 1
12.23
```

### Email

Generate an email address

```bash
$ echo "{{email}}" | phony --max 1
areus@example.org
```

### Event action

Generate an event action

```bash
$ echo "{{event.action}}" | phony --max 1
Viewed
```

### Http method

Generate a HTTP method

```bash
$ echo "{{http.method}}" | phony --max 1
GET
```

### Id

Generate an identifier

```bash
$ echo "{{id}}" | phony --max 1
az23eGE23e
```

### Ipv4

Generate an ipv4 address

```bash
$ echo "{{ipv4}}" | phony --max 1
10.23.45.67
```

### Ipv6

Generate an ipv6 address

```bash
$ echo "{{ipv6}}" | phony --max 1
2001:cafe:85:b:cf:62:60:81
```

### KSUID

Generate a k-sortable unique id

```bash
$ echo "{{ksuid}}" | phony --max 1
1Zlye1QoDrANrPV9MP6c1tMU4yd
```

### Latitude

Generate a geographical latitude

```bash
$ echo "{{latitude}}" | phony --max 1
-64.007899
```

### Longitude

Generate a geographical longitude

```bash
$ echo "{{longitude}}" | phony --max 1
-176.537284
```

### Mac address

Generate a mac address

```bash
$ echo "{{mac.address}}" | phony --max 1
cd:da:8d:e7:c5:e3
```

### Person name

Generate a person name

```bash
$ echo "{{name}}" | phony --max 1
Britta Mccarthy
```

### Firstname

Generate a firstname

```bash
$ echo "{{name.first}}" | phony --max 1
Filiberto
```

### Lastname

Generate a lastname

```bash
$ echo "{{name.last}}" | phony --max 1
Walton
```

### Product category

Generate a product category

```bash
$ echo "{{product.category}}" | phony --max 1
Clothing
```

### Product name

Generate a product name

```bash
$ echo "{{product.name}}" | phony --max 1
Namdax
```

### State

Generate a USA state

```bash
$ echo "{{state}}" | phony --max 1
Idaho
```

### State code

Generate the short code of a USA state

```bash
$ echo "{{state.code}}" | phony --max 1
AZ
```

### Timezone

Generate a timezone

```bash
$ echo "{{timezone}}" | phony --max 1
America/Phoenix
```

### Unixtime

Generate an Unix time

```bash
$ echo "{{unixtime}}" | phony --max 1
1585421720493623000
```

### Username

Generate a username

```bash
$ echo "{{username}}" | phony --max 1
kerem
```

### UUID

Generate an uuid

```bash
$ echo "{{uuid}}" | phony --max 1
f8b3a519-2e83-427f-b3a6-53e617310690
```

## License

  (MIT), 2014 Amir Abu Shareb.
