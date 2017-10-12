#行情数据

## 字典定义

### 市场代码

| 市场名称 | 市场代码 |
| --- | --- |
| 深交所 | SZ |
| 上交所 | SH |
| 中金所 | CFE |
| 郑商所 | CZC |
| 大商所 | DCE |
| 上期所 | SHF |
| 上金所 | SGE |
| 中证指数 | CSI |
| 港交所 | HK |


### 标的代码（symbol）

由标的原始代码加市场代码（表1）组合而成，中间以&#39;.&#39;隔开，如&#39;000001.SH&#39;，多标的输入时以逗号 (&#39;,&#39;) 隔开，如：&#39;000001.SH, cu1709.SHF&#39;

### 分钟线类型（freq）

| 分钟线类型 | 说明 |
| --- | --- |
| 15s | 15秒线 |
| 30s | 30秒线 |
| 1m | 1分钟线 |
| 5m | 5分钟线 |
| 15m | 15分钟线 |

## 实时行情数据查询 quote

输入标的代码（支持多标的），输出为最新市场行情，以dataframe格式返回，可指定返回字段，以fields参数标识。

查询示例：

```python
df, msg = api.quote(
				view="000001.SH, cu1709.SHF", 
				fields="open,high,low,last,volume")
```

输入参数：

1. **标的代码** ，支持多标的查询
2. 需要返回字段（fields），多字段以&#39;,&#39;隔开

| 字段 | 类型 | 说明 | 缺省 |
| --- | --- | --- | --- |
| symbol | string | [**标的代码**] [，支持多标的查询] | 不可缺省 |
| fields | string | 需要返回字段，多字段以&#39;,&#39;隔开；为&quot;&quot;时返回所有字段 | &quot;&quot; |


输出字段：

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| symbol | string | **标的代码** |
| code | string | 交易所原始代码 |
| date | int | 自然日,YYYYMMDD格式，如20170823 |
| time | int | 时间，精确到毫秒，如14:21:05.330记为142105330 |
| trade\_date | int | YYYYMMDD格式，如20170823 |
| open | double | 开盘价 |
| high | double | 最高价 |
| low | double | 最低价 |
| last | double | 最新价 |
| close | double | 收盘价 |
| volume | int | 成交量（总） |
| turnover | double | 成交金额（总） |
| vwap | double | 当日平均成交均价，计算公式为成交金额除以成交量 |
| oi | int | 持仓总量 |
| settle | double | 今结算价 |
| iopv | double | IOPV净值估值 |
| limit_up | double | 涨停价 |
| limit_down | double | 跌停价 |
| preclose | double | 昨收盘价 |
| presettle | double | 昨结算价 |
| preoi | int | 昨持仓 |
| askprice1 | double | 申卖价1 |
| askprice2 | double | 申卖价2 |
| askprice3 | double | 申卖价3 |
| askprice4 | double | 申卖价4 |
| askprice5 | double | 申卖价5 |
| bidprice1 | double | 申买价1 |
| bidprice2 | double | 申买价2 |
| bidprice3 | double | 申买价3 |
| bidprice4 | double | 申买价4 |
| bidprice5 | double | 申买价5 |
| askvolume1 | int | 申卖量1 |
| askvolume2 | int | 申卖量2 |
| askvolume3 | int | 申卖量3 |
| askvolume4 | int | 申卖量4 |
| askvolume5 | int | 申卖量5 |
| bidvolume1 | int | 申买量1 |
| bidvolume2 | int | 申买量2 |
| bidvolume3 | int | 申买量3 |
| bidvolume4 | int | 申买量4 |
| bidvolume5 | int | 申买量5 |


## 日线查询 daily

日线查询，支持停牌补齐、复权选择等选项。

输入参数：

1. **标的代码** ，支持多标的查询，必要参数
2. 开始日期 (start\_date), string或者int类型：若为string类型，格式&#39;YYYY-MM-DD&#39;，如&#39;2017-08-01&#39;；若为int类型，格式为YYYYMMDD，如20170801。必要参数。
3. 结束日期 (end\_date), string或者int类型：若为string类型，格式&#39;YYYY-MM-DD&#39;，如&#39;2017-08-01&#39;；若为int类型，格式为YYYYMMDD，如20170801。必要参数。
4. 复权类型(adjust\_mode)，string类型，&#39;pre&#39;为前复权，None不复权，&#39;post&#39;为后复权。缺省为None
5. 返回字段 (fields), 多字段以 &#39;,&#39; 隔开，缺省时全字段返回。可选参数。

| 字段 | 类型 | 说明 | 缺省值 |
| --- | --- | --- | --- |
| symbol | string | **标的代码** ，支持多标的查询 | 不可缺省 |
| start\_date | int或者string | 开始日期, int时为YYYYMMDD格式(如20170809)；string时为&#39;YYYY-MM-DD&#39;格式，如&#39;2017-08-09&#39; | 不可缺省 |
| end\_date | int或者string | 结束日期，int时为YYYYMMDD格式(如20170809)；string时为&#39;YYYY-MM-DD&#39;格式，如&#39;2017-08-09&#39; | 不可缺省 |
| adjust\_mode | string | &#39;pre&#39;为前复权，None不复权，&#39;post&#39;为后复权 | None |
| fields | string | 需要返回字段，多字段以&#39;,&#39;隔开,为&quot;&quot;时返回所有字段 | &quot;&quot; |


查询示例：
```python
df, msg = api.daily(
				symbol="600832.SH, 600030.SH", 
				start_date="2012-10-26",
				end_date="2012-11-30", 
				fields="", 
				adjust_mode="post")
```
返回字段：

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| symbol | string | **标的代码** |
| code | string | 交易所原始代码 |
| trade\_date | int | YYYYMMDD格式，如20170823 |
| open | double | 开盘价 |
| high | double | 最高价 |
| low | double | 最低价 |
| close | double | 收盘价 |
| volume | int | 成交量 |
| turnover | double | 成交金额 |
| vwap | double | 成交均价 |
| settle | double | 结算价 |
| oi | int | 持仓量 |
| trade\_status | string | 交易状态（&quot;停牌&quot;或者&quot;交易&quot;） |


## 分钟线查询 bar

查询各种类型的分钟线,支持日内及历史bar查询，以dataframe格式返回查询结果。

输入参数：

1. **标的代码** ，支持多标的查询，必要参数。
2. 开始时间 (start\_time), 精确到秒，string或者int类型：若为string类型，格式为&#39;HH:MM:SS&#39;，如&#39;09:32:35&#39;；若传入int类型，格式为HHMMSS，如93235。缺省为为开盘时间。
3. 结束时间 (end\_time), 精确到秒，string或者int类型：若为string类型，格式为&#39;HH:MM:SS&#39;，如&#39;09:32:35&#39;；若传入int类型，格式为HHMMSS，如9323。缺省为当前时间（日内）或者收盘时间（历史）。
4. 交易日 (trade\_date), string或者int类型：若为string类型，格式&#39;YYYY-MM-DD&#39;，如&#39;2017-08-01&#39;；若为int类型，格式为YYYYMMDD，如20170801。缺省为当前交易日。
5. **分钟线类型** (freq),缺省为一分钟线 (&#39;1m&#39;)。
6. 返回字段 (fields), 多字段以 &#39;,&#39; 隔开，缺省时全字段返回。

| 字段 | 类型 | 说明 | 缺省值 |
| --- | --- | --- | --- |
| symbol | string | **标的代码** ，支持多标的查询 | 不可缺省 |
| start\_time | int或string | 开始时间 | 开盘时间 |
| end\_time | int或string | 结束时间 | 收盘时间 |
| trade\_date | int或string | 交易日 | 当前交易日 |
| freq | string | 分钟线类型 | &quot;1m&quot; |
| fields | string | 需要返回字段，多字段以&#39;,&#39;隔开,为&quot;&quot;时返回所有字段 | &quot;&quot; |


查询示例：
```python
df,msg = api.bar(
			symbol="600030.SH", 
			trade_date=20170928, 
			freq="5m",
			start_time="00:00:00",
			end_time="16:00:00",
            fields="")
```
返回字段：

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| symbol | string | **标的代码** |
| code | string | 交易所原始代码 |
| date | int | 自然日,YYYYMMDD格式，如20170823 |
| time | int | 时间，精确到毫秒，如14:21:05.330记为142105330 |
| trade\_date | int | YYYYMMDD格式，如20170823 |
| freq | string | bar类型 |
| open | double | bar内开盘价 |
| high | double | bar内最高价 |
| low | double | bar内最低价 |
| close | double | bar内收盘价 |
| volume | int | bar内成交量 |
| turnover | double | bar内成交金额 |
| vwap | double | bar内成交均价 |
| oi | int | 当前持仓量 |
| settle | double | 结算价 |


## bar quote查询 bar_quote

在分钟线基础上再加入该分钟结束前最后一笔的行情信息（主要是ask,bid信息），以dataframe格式返回查询结果。

输入参数：

1. **标的代码** ，支持多标的查询，必要参数。
2. 开始时间 (start\_time), 精确到秒，string或者int类型：若为string类型，格式为&#39;HH:MM:SS&#39;，如&#39;09:32:35&#39;；若传入int类型，格式为HHMMSS，如93235。缺省为为开盘时间。
3. 结束时间 (end\_time), 精确到秒，string或者int类型：若为string类型，格式为&#39;HH:MM:SS&#39;，如&#39;09:32:35&#39;；若传入int类型，格式为HHMMSS，如9323。缺省为当前时间（日内）或者收盘时间（历史）。
4. 交易日 (trade\_date), string或者int类型：若为string类型，格式&#39;YYYY-MM-DD&#39;，如&#39;2017-08-01&#39;；若为int类型，格式为YYYYMMDD，如20170801。缺省为当前交易日。
5. **分钟线类型** (freq), 缺省为一分钟线 (&#39;1m&#39;)。
6. 返回字段 (fields), 多字段以 &#39;,&#39; 隔开，缺省时全字段返回。

| 字段 | 类型 | 说明 | 缺省值 |
| --- | --- | --- | --- |
| symbol | string | **标的代码** ，支持多标的查询 | 不可缺省 |
| start\_time | int或string | 开始时间 | 开盘时间 |
| end\_time | int或string | 结束时间 | 收盘时间 |
| trade\_date | int或string | 交易日 | 当前交易日 |
| freq | string | 分钟线类型 | &quot;1m&quot; |
| fields | string | 需要返回字段，多字段以&#39;,&#39;隔开,为&quot;&quot;时返回所有字段 | &quot;&quot; |


查询示例：

```python
df,msg = api.bar_quote(
					symbol="000001.SH,cu1709.SHF",  
					start_time = "09:56:00", 
					end_time="13:56:00", 
					trade_date=20170823, 
					freq= "5m",
					fields="open,high,low,last,volume")
```
返回字段：

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| symbol | string | **标的代码** |
| code | string | 交易所原始代码 |
| date | int | 自然日，YYYYMMDD格式，如20170823 |
| time | int | 时间，精确到毫秒，如14:21:05.330记为142105330 |
| trade\_date | int | 交易日，YYYYMMDD格式，如20170823 |
| freq | string | bar类型 |
| open | double | bar内开盘价 |
| high | double | bar内最高价 |
| low | double | bar内最低价 |
| close | double | bar内收盘价 |
| volume | int | bar内成交量 |
| turnover | double | bar内成交金额 |
| vwap | double | bar内成交均价 |
| oi | int | 当前持仓量 |
| settle | double | 结算价 |
| askprice1 | double | 申卖价1 |
| askprice2 | double | 申卖价2 |
| askprice3 | double | 申卖价3 |
| askprice4 | double | 申卖价4 |
| askprice5 | double | 申卖价5 |
| bidprice1 | double | 申买价1 |
| bidprice2 | double | 申买价2 |
| bidprice3 | double | 申买价3 |
| bidprice4 | double | 申买价4 |
| bidprice5 | double | 申买价5 |
| askvolume1 | int | 申卖量1 |
| askvolume2 | int | 申卖量2 |
| askvolume3 | int | 申卖量3 |
| askvolume4 | int | 申卖量4 |
| askvolume5 | int | 申卖量5 |
| bidvolume1 | int | 申买量1 |
| bidvolume2 | int | 申买量2 |
| bidvolume3 | int | 申买量3 |
| bidvolume4 | int | 申买量4 |
| bidvolume5 | int | 申买量5 |


## 历史行情数据查询 tick()

支持历史及日内行情数据查询，查询结果以dataframe返回。

输入参数：

1. **标的代码** ，支持多标的查询
2. 开始时间 (start\_time), 精确到秒，string或者int类型：若为string类型，格式为&#39;HH:MM:SS&#39;，如&#39;09:32:35&#39;；若传入int类型，格式为HHMMSS，如93235。缺省为为开盘时间。
3. 结束时间 (end\_time), 精确到秒，string或者int类型：若为string类型，格式为&#39;HH:MM:SS&#39;，如&#39;09:32:35&#39;；若传入int类型，格式为HHMMSS，如9323。缺省为当前时间（日内）或者收盘时间（历史）。
4. 交易日 (trade\_date), string或者int类型：若为string类型，格式&#39;YYYY-MM-DD&#39;，如&#39;2017-08-01&#39;；若为int类型，格式为YYYYMMDD，如20170801。缺省为当前交易日。
5. 返回字段 (fields), 多字段以 &#39;,&#39; 隔开，缺省时全字段返回。

| 字段 | 类型 | 说明 | 缺省值 |
| --- | --- | --- | --- |
| symbol | string | **标的代码** ，支持多标的查询 | 不可缺省 |
| start\_time | int或string | 开始时间 | 开盘时间 |
| end\_time | int或string | 结束时间 | 收盘时间 |
| trade\_date | int或string | 交易日 | 当前交易日 |
| fields | string | 需要返回字段，多字段以&#39;,&#39;隔开,为&quot;&quot;时返回所有字段 | &quot;&quot; |



查询示例：
```python
df, msg = api.tick(
			view="000001.SH, cu1709.SHF",  
			start_time = "09:56:00", 
			end_time="13:56:00", 
			trade_date="20170823", 
			fields="open,high,low,last,volume")
```
返回字段：

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| symbol | string | **标的代码** |
| code | string | 交易所原始代码 |
| date | int | 自然日,YYYYMMDD格式，如20170823 |
| time | int | 时间，精确到毫秒，如14:21:05.330记为142105330 |
| trade\_date | int | YYYYMMDD格式，如20170823 |
| open | double | 开盘价 |
| high | double | 最高价 |
| low | double | 最低价 |
| last | double | 最新价 |
| close | double | 收盘价 |
| volume | int | 成交量（总） |
| turnover | double | 成交金额（总） |
| vwap | double | 当日平均成交均价，计算公式为成交金额除以成交量 |
| oi | int | 持仓总量 |
| settle | double | 今结算价 |
| iopv | double | IOPV净值估值 |
| high\_limit | double | 涨停价 |
| low\_limit | double | 跌停价 |
| preclose | double | 昨收盘价 |
| presettle | double | 昨结算价 |
| preoi | int | 昨持仓 |
| askprice1 | double | 申卖价1 |
| askprice2 | double | 申卖价2 |
| askprice3 | double | 申卖价3 |
| askprice4 | double | 申卖价4 |
| askprice5 | double | 申卖价5 |
| bidprice1 | double | 申买价1 |
| bidprice2 | double | 申买价2 |
| bidprice3 | double | 申买价3 |
| bidprice4 | double | 申买价4 |
| bidprice5 | double | 申买价5 |
| askvolume1 | int | 申卖量1 |
| askvolume2 | int | 申卖量2 |
| askvolume3 | int | 申卖量3 |
| askvolume4 | int | 申卖量4 |
| askvolume5 | int | 申卖量5 |
| bidvolume1 | int | 申买量1 |
| bidvolume2 | int | 申买量2 |
| bidvolume3 | int | 申买量3 |
| bidvolume4 | int | 申买量4 |
| bidvolume5 | int | 申买量5 |


