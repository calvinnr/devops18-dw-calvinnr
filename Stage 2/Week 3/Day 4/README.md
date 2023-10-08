# Monitoring
## 1. Dashboard untuk monitor resource server (CPU, RAM & Disk Usage)
### 1.1 Konfigurasi Dashboard

<img width="1440" alt="Screenshot 2023-10-09 at 04 31 25" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/a7d10cd7-f7f8-4f01-96f5-2798482f33db">

Pada tampilan utama Dashboard Grafana, Disini klik pada **DATA SOURCES / ADD YOUR FIRST DATA SOURCES**

<img width="1440" alt="Screenshot 2023-10-09 at 04 31 43" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/f938137b-6b62-4169-a73f-75d048c8349d">

Setelah itu klik **Prometheus**

<img width="1440" alt="Screenshot 2023-10-09 at 04 32 45" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/d5012a6c-81ad-49b7-b190-7152ad72591c">
<img width="1440" alt="Screenshot 2023-10-09 at 04 34 40" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/9d11c84b-6ab4-4803-8eba-8d59e48473d2">
<img width="1440" alt="Screenshot 2023-10-09 at 04 34 55" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/4c08e848-8c63-4df2-b2df-7ec4e41c97c6">

Berikut beberapa konfigurasi yang saya ribuh

> Name: Prometheus
>
> Prometheus server URL: http://prometheus.calvin.studentdumbways.my.id
>
> Scrape interval: 10s
>
> Query timeout: 60s
>
> Default editor: Code
>
> Prometheus type: Prometheus

Lalu save hasil konfigurasi Data Source-nya.

<br>

<img width="1440" alt="Screenshot 2023-10-09 at 04 35 39" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/a3be3324-c627-4511-a654-4e7374847a83">

Setelah Data Source-nya terbuat, klik pada **Build a Dashboard**

<br>

<img width="1440" alt="Screenshot 2023-10-09 at 04 35 46" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/0479c0ca-2111-464e-93f4-422da21c81b0">

Lalu klik **Add visualization**

<br>

<img width="1440" alt="image" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/9cd1e46c-a408-4a08-9b31-264fc214988a">

Berikut query untuk RAM Usage:

```grafana
100 * (1 - ((avg_over_time(node_memory_MemFree_bytes[10m]) + avg_over_time(node_memory_Cached_bytes[10m]) + avg_over_time(node_memory_Buffers_bytes[10m])) / avg_over_time(node_memory_MemTotal_bytes[10m])))
```

<img width="1440" alt="Screenshot 2023-10-09 at 05 27 15" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/52966d58-4bc0-4947-aac6-be2f4961fc29">

Berikut query untuk CPU Usage:

```grafana
100 - (avg by(instance) (irate(node_cpu_seconds_total{mode="idle", job="appserver"}[5m])) * 100)
```

<img width="1440" alt="Screenshot 2023-10-09 at 05 28 19" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/9cad13a6-2cfa-4afc-914f-676dc092a1dd">

Berikut query untuk Disk Usage:

```grafana
100 - (node_filesystem_avail_bytes / node_filesystem_size_bytes * 100)
```

<img width="1440" alt="Screenshot 2023-10-09 at 05 06 20" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/49f3e27f-3091-40f9-a0c3-949e2793da38">

Ini tampilan Dashboard setelah semua Query dijalankan dan sudah disimpan dengan nama `Monitoring Appserver & Gateway`
