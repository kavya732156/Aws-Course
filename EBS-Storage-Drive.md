***EBS provide 3 Categories of storage Drives***
***1. SSD (Solid State Drives) – Low Latency, High IOPS***
  a. Stands For Solid State Drive
  b. SSD is Durable, Faster, More Energy Efficient
  c. It is used for Performing tasks like Booting & Loading Applications.
  d. Very Fast Processing for Low Data
  e. Small in Size 
  f. SSD’s are Most Costlier than HDD the performance of the SSD is measured in terms of IOPS [ Input & Output operations per second].

  ***Types:***
  1. ***gp3 / gp2 → General Purpose SSD*** : Which is Used For Normal Access
     gp2--- 100 IOPS > 16000 IOPS = 16TB
     gp3.... 3000 IOPS > 16000 IOPS = 16TB

  2. ***io2 / io1 → Provisioned IOPS SSD*** : Which is Used For rapid access
     io1- 100 IOps > 64000 Iops =64 tb
     io2 - 100 IOps > 64000 Iops = 64 tb
     io2 Block express r5-b instance type--more than 64000 Iops > 64TB

***2. HDD (Hard Disk Drives) – High Throughput, Low Cost***
   a. HDD stands for Hard Disk Drive
   b. It is a Type of Storage Device.
   c. Compare to SSD, HDD are Slower & Less Energy Efficient but they are tend to affordable at Higher Storage Capacities
   d. Big in Size
   e. Low Cost disk drives

   ***Types:***
   ***1. st1 → Throughput Optimized HDD***
   a. A low-cost HDD designed for frequently accessed, throughput-intensive workloads.
   b. Min: 125 GiB, Max: 16384 GiB.
   c. Throughput  Baseline starts with 40 MiB/s per TiB.

   ***2. sc1 → Cold HDD***
   a. The lowest-cost HDD design for less frequently accessed workloads.
   b. Min: 125 GiB, Max: 16384 GiB.
   c. Throughput  Baseline starts with 12 MiB/s per TiB.

***3. Magnetic (Standard) – Legacy (Deprecated-ish)***
   a. Old generation EBS (avoid for new workloads)
   b. Lowest cost (old days)
   c. High latency
   d. Low performance
   e. Not recommended for new setups

   ***Type:***
   1. standard (magnetic)
      a. usecase : Workloads where data is infrequently accessed
      b. Volume size	: 1 GiB-1 TiB
      c. Max IOPS per volume	40–200
      d. Max throughput per volume	40–90 MiB/s
      e. Boot volume	Supported
