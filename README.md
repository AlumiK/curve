# Curve

Curve is an open source tool to help label anomalies on time series data. The labeled data (also known as the ground truth) is necessary for evaluating time series anomaly detection methods. Otherwise, one can not easily choose a detection method, or say method A is better than method B. The labeled data can also be used as the training set if one wants to develop supervised learning methods for detection.

Curve is designed to support plugin, so one can equip Curve with customized and powerful functions to help label effectively. For example, a plugin to identify anomalies which are similar to the one you labeled, so you don't have to search them through all the data.

Curve is originally developed by Baidu and Tsinghua NetMan Lab.

![](https://raw.githubusercontent.com/AlumiK/curve/master/doc/pic/index.png)

## Getting Started

### Dependencies

Linux(Ubuntu, CentOS, Arch, etc.) or Darwin(Mac OSX) is recommended.

- Python 2.7
- Node.js
- GCC
- virtualenv

### Run

Simply use `control.sh` to start or stop Curve.

```
./control.sh start
./control.sh stop
```

Server will blind port 8080 by default. You can change it in `./api/uwsgi.ini`.

The first start will take a while because of the compilation. If you pull updates from GitHub, a rebuild will be triggered during start or reload.

### Data Format

You can load CSV files into Curve. The CSV should have the following format:

- The first column is the timestamps.
- The second column is the values.
- The third column (optional) is the label. `0` for normal points and `1` for anomaly points.

The headers of CSV is optional, like `timestamp,value,label`.  

Some examples of valid CSV:

- With headers and the label column.

|timestamp|value|label|
| - | - | - |
|1476460800|2566.35|0|
|1476460860|2704.65|0|
|1476460920|2700.05|0|


- Without headers.

<table>
    <tr>
        <td>1476460800</td>
        <td>2566.35</td>
        <td>0</td>
    </tr>
    <tr>
        <td>1476460860</td>
        <td>2704.65</td>
        <td>0</td>
    </tr>
    <tr>
        <td>1476460920</td>
        <td>2700.05</td>
        <td>0</td>
    </tr>
</table>

* Without headers and the label column.

<table>
    <tr>
        <td>1476460800</td>
        <td>2566.35</td>
    </tr>
    <tr>
        <td>1476460860</td>
        <td>2704.65</td>
    </tr>
    <tr>
        <td>1476460920</td>
        <td>2700.05</td>
    </tr>
</table>

* Timestamps in human-readable format.

<table>
    <tr>
        <td>20161015000000</td>
        <td>2566.35</td>
    </tr>
    <tr>
        <td>20161015000100</td>
        <td>2704.65</td>
    </tr>
    <tr>
        <td>20161015000200</td>
        <td>2700.05</td>
    </tr>
</table>

## Additional

### Backend Unit Test

```
cd api && pytest
```

### Plugin Path

```
./api/curve/v1/plugins
```

### GitHub OAuth

GitHub OAuth is supported, please put a configuration file in `api/curve/auth/github_oauth.json` like this:

```json
{
  "id": "your GitHub application Client ID",
  "secret": "your application Client Secret"
}
```

See [Creating an GitHub OAuth App](https://docs.github.com/en/free-pro-team@latest/developers/apps/creating-an-oauth-app) for more information.
