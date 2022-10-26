# Import utilities

Utilities to help with importing existing resources into this module

## Security group rules importer

This utility generates the `ingress_with_cidr_blocks` and `egress_with_cidr_blocks` Terraform blocks used by this module. It also produces the Terraform import commands to import existing security groups rules into local state.

Usage: `python tf-import-prep-sgr.py sg-0cf26d36ab3c9ae4a`

Example output

```
ingress_with_cidr_blocks = [
  {
    description = "SMB USB"
    from_port = 137
    to_port = 137
    protocol = "udp"
    cidr_blocks = "10.0.0.0/32"
  },
  {
    description = "DNS"
    from_port = 53
    to_port = 53
    protocol = "udp"
    cidr_blocks = "10.72.0.0/32"
  },
]

egress_with_cidr_blocks = [
  {
    description = "Allow all outbound"
    from_port = -1
    to_port = -1
    protocol = "-1"
    cidr_blocks = "0.0.0.0/0"
  },
]

terraform import module.baseline_sg.aws_security_group_rule.ingress_with_cidr_blocks[0] sg-0cf26d36ab3c9ae4a_ingress_udp_137_137_10.0.0.0/32
terraform import module.baseline_sg.aws_security_group_rule.ingress_with_cidr_blocks[1] sg-0cf26d36ab3c9ae4a_ingress_udp_53_53_10.72.0.0/32
terraform import module.baseline_sg.aws_security_group_rule.egress_with_cidr_blocks[0] sg-0cf26d36ab3c9ae4a_egress_-1_-1_-1_0.0.0.0/0
```
