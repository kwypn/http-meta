# HTTP META

## Usage

## The Easy Way(for example, on an Android device)

Create a folder `/data/http-meta`

Download [http-meta.bundle.js](https://github.com/xream/http-meta/releases/latest/download/http-meta.bundle.js), rename it to `http-meta.bundle.js`and move it to the `/data/http-meta` folder.

Create a folder `/data/http-meta/meta`

Download [Meta](https://github.com/MetaCubeX/mihomo/releases), rename it to `http-meta` and move it to the `/data/http-meta/meta` folder.

Download [tpl.yaml](https://github.com/xream/http-meta/releases/latest/download/tpl.yaml), rename it to `tpl.yaml` and move it to the `/data/http-meta/meta` folder.

> `META_FOLDER` can be the absolute path of the `meta` folder if neccessary.

`META_FOLDER=/data/http-meta/meta HOST=127.0.0.1 PORT=9876 node http-meta.bundle.js`

## The Hard Way

`cd /data`

`git clone https://github.com/xream/http-meta.git http-meta`

`cd /data/http-meta`

Download [Meta](https://github.com/MetaCubeX/mihomo/releases), rename it to `http-meta` and move it to the `/data/http-meta/meta` folder.

`cd /data/http-meta`

`pnpm i`

> `META_FOLDER` can be the absolute path of the `meta` folder if neccessary.

`META_FOLDER=/data/http-meta/meta HOST=127.0.0.1 PORT=9876 pnpm start`

## Start (always start a new one)

```console
curl '127.0.0.1:9876/start' \
--header 'Content-Type: application/json' \
--data '{
    "timeout": 1800000, // process will be killed after 30 minutes(default)
    "proxies": [
        {
            "name": "1",
            "server": "1.2.3.4",
            "port": 80,
            "type": "vmess",
            ...
        }
    ]
}'
```

### Response

```JSON
{
    "ports": [
        65534,
        65533
    ],
    "pid": 61289
}
```

## Retart(stop all and start a new one)

```console
curl '127.0.0.1:9876/start' \
--header 'Content-Type: application/json' \
--data '{
    "timeout": 1800000, // process will be killed after 30 minutes(default)
    "proxies": [
        {
            "name": "1",
            "server": "1.2.3.4",
            "port": 80,
            "type": "vmess",
            ...
        },
          {
            "name": "2",
            "server": "1.2.3.4",
            "port": 80,
            "type": "vmess",
            ...
        }
    ]
}'
```

### Response

```JSON
{
    "ports": [
        65534,
        65533
    ],
    "pid": 61289
}
```

## Stop

### Stop All

```console
curl --request POST '127.0.0.1:9876/stop'
```

### Stop by PID

```console
curl '127.0.0.1:9876/stop' \
--header 'Content-Type: application/json' \
--data '{
    "pid": [
        1,
        2
    ]
}'
```

### Response

```JSON
{
    "pid": null
}
```

## Get Stats

```console
curl '127.0.0.1:9876/stats' \
--header 'Content-Type: application/json'
```

### Response

```JSON
{
    "35955": {
        "pid": 35955,
        "mem": "2MB",
        "cpu": "0%"
    }
}
```

## Get Stats by PID

```console
curl '127.0.0.1:9876/stats' \
--header 'Content-Type: application/json' \
--data '{"pid": [35955]}'
```

### Response

```JSON
{
    "35955": {
        "pid": 35955,
        "ports": [
            65534,
            65533
        ],
        "mem": "2MB",
        "cpu": "0%"
    }
}
```
