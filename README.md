# perfana-jmeter-demo-script

jMeter script demo for Perfana performance test dashboard using the Afterburner demo application.

Start test with ```mvn -U verify``` and use a Maven profile to set test environment and workload, e.g.

```bash
mvn -U verify -Ptest-env-local,test-type-load
```

### background info
The `-U` option is to always fetch the latest versions of the Perfana event plugins via the Maven version range construct.
If omitted Maven does not seem to update the local `maven-metadata.xml` files. 

