
###Drools Commands
#####BatchExecutionCommand
包含其他多个命令的命令，一个API请求最外层的参数，有以下属性：
* lookup, 每次跟规则引擎会话都会有一个session id
* commands，执行的若干命令

XML output
```xml
	<batch-execution lookup='ksession1'>
		//other commands
	</batch-execution>
```
#####InsertObjectCommand
插入的数据，这些数据需要跟drools的数据对象对应，包括每个数据项的数据类型，否则会报错
XML output
```xml
	<insert>
		<test.account>
			<balance>123.45</balance>
			<name>Jack</name>
		</test.account>
	</insert>
```
#####RetractCommand
收回某个数据，需要提供收回数据对象的handle
```xml
	<retract fact-handle='0:234:345:456:567' />
```
#####ModifyCommand
更新某个数据对象，需要提供更新对象的handle
```xml
	<modify fact-handle='0:234:345:456:567'>
		<set accessor='balance' value=10000.00 />
		<set accessor='name' value='Jone' />
	</modify>
```
#####GetObjectCommand
获取某个对象，需要提供数据对象的handle
```xml
	<get-object fact-handle='0:234:345:456:567' out-indentifier='jone' />
```
#####InsertElementsCommand
插入批量插入多个对象
```xml
	<insert-elements>
		<test.account>
			<balance>999.99</balance>
			<name>Jack</name>
		</test.account>
		<test.account>
			<balance>111111.11</balance>
			<name>Lucy</name>
		</test.account>
	</insert-elements>
```
#####StartProcessCommand
开始执行的业务流程id
```xml
	<start-process processId='test.account.workflow.AccountWorkFlow' />
```
完整实例
```xml
<batch-execution lookup="ksession1">
  <insert>
      <cloudoc.glucose.Patient>
          <isDiabetes>true</isDiabetes>
          <isInsulinUsed>true</isInsulinUsed>
      </cloudoc.glucose.Patient>
  </insert>
  <insert>
      <cloudoc.glucose.Record>
        <value>5.0</value>
        <acktype>1</acktype>
      </cloudoc.glucose.Record>
  </insert>
  <insert>
      <cloudoc.glucose.Record>
        <value>3.0</value>
        <acktype>0</acktype>
      </cloudoc.glucose.Record>
  </insert>
  <insert>
      <cloudoc.glucose.Record>
        <value>10.2</value>
        <acktype>3</acktype>
      </cloudoc.glucose.Record>
  </insert>
  <insert>
      <cloudoc.glucose.Record>
        <value>18.5</value>
        <acktype>4</acktype>
      </cloudoc.glucose.Record>
  </insert>
  <insert>
      <cloudoc.glucose.Statistic>
          <fbgCount>0</fbgCount>
          <fbgNormalCount>0</fbgNormalCount>
          <twoHpgCount>0</twoHpgCount>
          <twoHpgNormalCount>0</twoHpgNormalCount>
          <hypoglycemiaCount>0</hypoglycemiaCount>
          <hyperglycemiaCount>0</hyperglycemiaCount>
          <averageFBG>0.0</averageFBG>
          <fbgStandardDeviation>0.0</fbgStandardDeviation>
          <fbgVariance>0.0</fbgVariance>
          <averageTwoHpg>0.0</averageTwoHpg>
          <twoHpgStandardDeviation>0.0</twoHpgStandardDeviation>
          <twoHpgVariance>0.0</twoHpgVariance>
      </cloudoc.glucose.Statistic>
  </insert>
  <start-process processId="glucose.glucoseWorkFlow2"/>
  <fire-all-rules/>
  <get-objects out-identifier="objects"/>

</batch-execution>
```