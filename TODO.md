# new conformance failures

## duration same sign

```
{ '$typeName': 'google.protobuf.Duration', seconds: 1n, nanos: -1 }
```

```
ERROR, test=Required.Proto3.DurationProtoNanosWrongSign.JsonOutput: Should have failed to serialize, but didn't., request=goo.gle/debugproto    protobuf_payload: "\352\022\r\010\001\020\377\377\377\377\377\377\377\377\377\001" requested_output_format: JSON message_type: "protobuf_test_messages.proto3.TestAllTypesProto3" test_category: JSON_TEST, response=goo.gle/debugproto    json_payload: "{\"optionalDuration\":\"1.000000001s\"}"
```

This (and the next) requires an additional check in durationToJson(), and probably a fix in durationFromMs().
Also check timestampFromMs()


## duration same sign 2

```
optionalDuration: { '$typeName': 'google.protobuf.Duration', seconds: -1n, nanos: 1 }
```

```
ERROR, test=Required.Editions_Proto3.DurationProtoNanosWrongSignNegativeSecs.JsonOutput: Should have failed to serialize, but didn't., request=goo.gle/debugstr   protobuf_payload: "\352\022\r\010\377\377\377\377\377\377\377\377\377\001\020\001" requested_output_format: JSON message_type: "protobuf_test_messages.editions.proto3.TestAllTypesProto3" test_category: JSON_TEST, response=goo.gle/debugstr   json_payload: "{\"optionalDuration\":\"-1.000000001s\"}"
```

## timestamp nanos too large

```
optionalTimestamp: {
'$typeName': 'google.protobuf.Timestamp',
seconds: 5000n,
nanos: 1000000000
}
```

```
ERROR, test=Required.Proto3.TimestampProtoNanoTooLarge.JsonOutput: Should have failed to serialize, but didn't., request=goo.gle/debugonly   protobuf_payload: "\362\022\t\010\210\'\020\200\224\353\334\003" requested_output_format: JSON message_type: "protobuf_test_messages.proto3.TestAllTypesProto3" test_category: JSON_TEST, response=goo.gle/debugonly   json_payload: "{\"optionalTimestamp\":\"1970-01-01T01:23:20.000Z\"}"
```

