[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: TSANG Ki Ka
### Student Id: 21133965
### Email: kktsangaf@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > Phoronix Test Suite is used in this assignment.  I configured it by selecting benchmark tests designed for CPU and memory performance analyzation.  In CPU benchmark, I set 7 zip compression test while in memory benchmark, I set RAM speed copy integer test.  For both 7 zip compression test and RAM speed copy integer test, I have set to iterate 3 times and take the average.  I have set MIPS and MB/S as the value obtained of the test respectively.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro`  |      3507       |   10615.28         |
    | `t2.medium` |      9758       |   19347.62         |
    | `c5d.large` |      7839       |   14319.87         |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.
    > To conclude, the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource generally desides the last one.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |    23600       |   0.0292 |
    | `m5.large` - `m5.large`   |      31400     |   0.0225 |
    | `c5n.large` - `c5n.large` |      34600     |   0.0206 |
    | `t3.medium` - `c5n.large` |      2190      |   0.913  |
    | `m5.large` - `c5n.large`  |      4950      |   0.1478 |
    | `m5.large` - `t3.medium`  |     2190       |   0.7446 |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.
    > Ans: Remark: RTT is calculated by taking the RTTs' average of the first 5 round icmp sequence.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |  40500         |   0.0971 |
    | N. Virginia - N. Virginia |  40300         |   0.0218 |
    | Oregon - Oregon           |  40100         |   0.0192 |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
    > Ans: Remark: RTT is calculated by taking the RTTs' average of the first 5 round icmp sequence.
