# ADR [001]: Security Risk Denial of Service (DDoS) Attack

## Context

Mule Apps or other web apps could be targeted and receive enormous amounts of requests.
If an attacker can flood the network or the server with millions of requests, physical resources like the CPU or the network bandwith could collapse.

The company needs the APIs and other software components to stay available 24/7, therefore, this type of attack must be mitigated.

## Decision

The mule apps are running in Cloudhub 2.0, in order to mitigate this attack we need to do the following:

- Identify when this attack is ocurring. Anypoint Monitoring might help, defining an alert if there's a surge in traffic.
- Provide enough infrastructure to handle the real end users traffic. Make sure there's enough vCores for mule apps, or UBP traffic on the license.
- Block the bad actors (attackers/hackers) from the origin IP address. Use API Manager with the policy IP Blocklist, and block bad actors IPs
- Alternatively, APIs could be restricted to be consumed only from a certain group of IPs using API Manager IP Allowlist.
- Additionaly, in Cloudhub 2.0 we could using a DLB (dedicated load balancer, officially called Ingress) that could use HTTPS (mutual TLS) to allow only clients with the valid client certificate.
- 

## Status

Proposed

## Consequences

Positive consequences:
- Improved security, with a more efficient use of the resources and attack mitigation techniques

Negative impact:
- The use of HTTPS (mutual SSL mTLS) could reduce the API performance (example like 20%)
- If the strategy classifies a real end user as an attacker, could block real users traffic.
- 

## Related documents

[List any related documents, such as requirements or design documents, that influenced the decision.]

### References
- https://github.com/joelparkerhenderson/architecture-decision-record
- https://github.com/joelparkerhenderson/architecture-decision-record/blob/main/examples/metrics-monitors-alerts/index.md
- https://github.com/pmerson/ADR-template
- https://github.com/joelparkerhenderson/architecture-decision-record/blob/main/examples/timestamp-format/index.md
- https://cloud.google.com/architecture/architecture-decision-records
