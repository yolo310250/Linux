## P4 language

- 參考

[簡單介紹 P4 語言](https://takeshi.tw/%E7%B0%A1%E5%96%AE%E4%BB%8B%E7%B4%B9-p4-%E8%AA%9E%E8%A8%80%EF%BC%88%E4%B8%80%EF%BC%89/)


### 實驗

- p4app.json
```
{

  "program": "basic.p4",

  "switch": "simple_switch",

  "compiler": "p4c",

  "options": "--target bmv2 --arch v1model --std p4-16",

  "switch_cli": "simple_switch_CLI",

  "cli": true,

  "pcap_dump": true,

  "enable_log": true,

  "topo_module": {

    "file_path": "",

    "module_name": "p4utils.mininetlib.apptopo",

    "object_name": "AppTopoStrategies"

  },

  "controller_module": null,

  "topodb_module": {

    "file_path": "",

    "module_name": "p4utils.utils.topology",

    "object_name": "Topology"

  },

  "mininet_module": {

    "file_path": "",

    "module_name": "p4utils.mininetlib.p4net",

    "object_name": "P4Mininet"

  },

  "topology": {

    "assignment_strategy": "l2",

    "links": [["h1", "s1"], ["h2", "s1"]],

    "hosts": {

      "h1": {

      },

      "h2": {

      }

    },

    "switches": {

      "s1": {

        "cli_input": "cmd.txt",

        "program": "basic.p4"

      }

    }

  }

}
```
- basic.p4
```
/* -*- P4_16 -*- */
#include <core.p4>
#include <v1model.p4>

/*************************************************************************
*********************** H E A D E R S  ***********************************
*************************************************************************/

struct metadata {
    /* empty */
}



struct headers {
}



/*************************************************************************
*********************** P A R S E R  ***********************************
*************************************************************************/

parser MyParser(packet_in packet,
                out headers hdr,
                inout metadata meta,
                inout standard_metadata_t standard_metadata) {

    state start {
        transition accept;
    }

}



/*************************************************************************

************   C H E C K S U M    V E R I F I C A T I O N   *************

*************************************************************************/



control MyVerifyChecksum(inout headers hdr, inout metadata meta) {  
    apply {  }
}

/*************************************************************************
**************  I N G R E S S   P R O C E S S I N G   *******************
*************************************************************************/
control MyIngress(inout headers hdr,
                  inout metadata meta,
                  inout standard_metadata_t standard_metadata) {
    action drop() {
        mark_to_drop(standard_metadata);
    }

    action forward(bit<9> port) {
        standard_metadata.egress_spec = port;
    }

    table phy_forward {
        key = {
            standard_metadata.ingress_port: exact;
        }

        actions = {
            forward;
            drop;
        }
        size = 1024;
        default_action = drop();
    }

    apply {
        phy_forward.apply();
    }
}

/*************************************************************************
****************  E G R E S S   P R O C E S S I N G   *******************
*************************************************************************/

control MyEgress(inout headers hdr,
                inout metadata meta,
                inout standard_metadata_t standard_metadata) {
    apply {  }
}

/*************************************************************************
*************   C H E C K S U M    C O M P U T A T I O N   **************
*************************************************************************/

control MyComputeChecksum(inout headers  hdr, inout metadata meta) {
    apply {
    }
}

/*************************************************************************
***********************  D E P A R S E R  *******************************
*************************************************************************/

control MyDeparser(packet_out packet, in headers hdr) {
    apply {
    }
}

/*************************************************************************
***********************  S W I T C H  *******************************
*************************************************************************/

V1Switch(
MyParser(),
MyVerifyChecksum(),
MyIngress(),
MyEgress(),
MyComputeChecksum(),
MyDeparser()

) main;
```

- cmd.txt
```
table_add phy_forward forward 1 => 2

table_add phy_forward forward 2 => 1
```

- 執行
    - p4run
    - h1 ping h2 -c 3


- 連接到p4交換機 
    - `simple_switch_CLI --thrift-port 9090`:預設為9090port通訊

    - `table_dump mac_forward`:查看table資訊
    - `table_clear mac_forward`:清除table資訊