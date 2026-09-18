# Korean Map pack for Subway Builder
Korean Map Pack (KMP) is a map mod for Subway Builder with real-world demand maps for 16 Korean cities, built from national transport and population statistics.

## Supported Cities
| City | 도시 | Code | Size |
|------|------|------|------|
| Seoul | 서울 | SEL | 40km |
| Incheon | 인천 | ICN | 40km |
| Busan | 부산 | PUS | 40km |
| Daegu | 대구 | TAE | 40km |
| Daejeon | 대전 | DAJ | 40km |
| Gwangju | 광주 | KWJ | 40km |
| Sejong | 세종 | SEJ | 40km |
| Ulsan | 울산 | USN | 40km |
| Jeju | 제주 | CJU | Full Island |
| Suwon | 수원 | SWU | 40km |
| Cheongju | 청주 | CJJ | 40km |
| Changwon | 창원 | CWN | 40km |
| Gyeongju–Pohang | 경주-포항 | KPO | 50km combined |
| Gangneung | 강릉 | KAG | 40km |
| Chuncheon | 춘천 | QCN | 40km |
| Jeonju–Gunsan–Iksan | 전주-군산-익산 | CHN | 92km×71km combined |

## Features
- **Sub-500m population placement** using Korea's national 500m population mesh
- **Commuter demand from KTDB** — origin-destination statistics from the Korea Transport Database, capturing real-world commute flows between traffic analysis zones
- **Road network routing** using actual Korean road centerline data, producing realistic driving paths between residential and employment points
- **Three-tier administrative labels** with English romanization
  - 시도 (Si, Do — Metropolitan / Provincial level)
  - 시군구 (Si, Gun, Gu — City / County / District level)
  - 읍면동 (Eup, Myeon, Dong — Neighborhood level)
- **Special demand POIs** — Airport, HSR station, Bus terminal, University, Hospital, School, Park, Shopping Center, Tourist Attraction, Ferry Terminal (where applicable); each modeled with real ridership, catchment gravity, enrollment, or visitor data
- **One map per city** — each city ships a single map at its largest size (40km, except Gyeongju–Pohang's 50km combined map, Jeju's Full Island map, and the Jeonju–Gunsan–Iksan combined map)

## Methodology
- Resident and commuter totals are approximated using KTDB traffic analysis zone data, spatially disaggregated via 500m population mesh grids to achieve sub-zone point placement.
- OD pairs are ranked by total trip volume and driving paths are computed via road network routing on the national road centerline dataset.
- Special demand points (airports, HSR stations, bus terminals, universities, hospitals) use mode-split rates, gravity models, and published ridership/enrollment statistics to generate realistic inbound and outbound flows.

## Primary Data Sources
- Korean Transportation Database (Korea Transport Institute, KOTI) — ktdb.go.kr
- V-world (Ministry of Land, Infrastructure and Transport, MOLIT) — vworld.kr
- Statistical Geographic Information System (SGIS) plus (Ministry of Data and Statistics, MODS) — sgis.mods.go.kr
- Address-based Industry Support Service (Ministry of the Interior and Safety, MOIS) — business.juso.go.kr
- Aviation statistics 2025 (Korea Civil Aviation Association, KCAA) — airportal.go.kr
- Korean railroad statistics 2024 (Korea Railroad, KORAIL) — railstat.korail.com
- Korean Public Transportation Database (Korea Transportation Safety Authority, KTSA) — kotsa.or.kr
- Korean Hospital and Pharmacy Status (Health Insurance Review and Assessment Service, HIRA) — data.go.kr
- Health Insurance Medical Statistics (HIRA) — opendata.hira.or.kr
- Academy Information System (Ministry of Education, MOE) — academyinfo.go.kr
- School Info Disclosure and Korea National Standard Data (schools, parks, shopping centers, tourist attractions) — schoolinfo.go.kr, data.go.kr
- Korea Transport Safety Authority (KOMSA) coastal ferry statistics — komsa.or.kr

---

## Update History
- **v0.4.0** — Added the Jeonju–Gunsan–Iksan combined map (16th city). Regenerated all travel demand from 2024 KTDB baseline data. Added school, park, shopping center, tourist attraction, and ferry terminal demand to every map. Fixed inconsistent English romanization on some place labels, a resident-count mismatch affecting POI-based demand, missing Chungnam-region buildings on 4 maps, and out-of-memory crashes during generation for large cities.
- **v0.3.1** — Added 6 minor cities (Suwon, Cheongju, Changwon, Gyeongju–Pohang, Gangneung, Chuncheon), each shipping as a single map. Introduced the Gyeongju–Pohang 50km dual-city composite map. Every city now ships one map at its largest size (map codes dropped their size suffix), fixed missing ocean rendering on coastal maps and missing buildings on the Gwangju map, restored low-rise buildings pack-wide, and upgraded water/greenery data to official government sources.
- **v0.2.0** — Added special demand modeling for airports, HSR stations, bus terminals, universities, and hospitals. Introduced zone-pair top-N demand selection and per-city config parameters.
- **v0.1.1** — Bug fixes for demand display and greenery layer rendering; improved demand distribution and OSRM travel time routing.

## Issues / Questions
Please report suggestions and issues via the [Discord Channel](https://discord.com/channels/1420846272545296470/1488123736270831717).

## Further Update Plan
- **v0.5.0: Metropolitan Maps** — Busan Metropolitan (Busan + Ulsan + Changwon), Daejeon Metropolitan (Daejeon + Sejong + Cheongju).
- Further plan: Add Seoul Metropolitan.
