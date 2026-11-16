# Autonomous Trailer – Knowledge-Based Agent

Deliverable: `Autonomous_Trailer.ipynb` following the 10-step knowledge-engineering template
(AllanVikiru/ArtificialIntelligence @ `kba`) and reusing Practical Exercise 3
(Nairobi road network, BFS/UCS, `search` branch).

## Plan
- [x] Read template notebook (kba branch) and Practical Exercise 3 (search branch)
- [x] Probe knowledge sources: Nominatim (geocoding), Overpass (OSM speed/height tags), Open-Meteo (weather)
- [x] Verify legal facts (Kenya trailer speed cap 65 km/h, EAC 56 t GVW / 7 axles)
- [x] Build notebook
  - [x] Step 1 task / PEAS / KB-agent architecture
  - [x] Step 2 knowledge acquisition (APIs + cached snapshot fallback, provenance)
  - [x] Step 3 vocabulary (predicates, constants)
  - [x] Step 4 general knowledge: directed road graph + Horn-clause rule base + inference engine (forward/backward chaining) + distance measures
  - [x] Step 5 add new facts (programmatic, API at run time, interactive with validation)
  - [x] Step 6/7 problem instance, BFS/UCS/Greedy/A* with drawn search tree, drive simulation with replanning
  - [x] Step 8 query interface (command language, explanations, interactive console)
  - [x] Step 9 debugging suite (rules, hygiene, graph integrity, heuristic admissibility, search vs Dijkstra, geo sanity, edge cases)
  - [x] Step 10 reflection
- [x] Execute notebook end-to-end headless (INTERACTIVE=False), confirm no errors, save outputs

## Review
- Headless run (nbclient, live APIs): 39 cells, 0 errors, 0 warnings, 3 figures; nbformat validates.
- Interactive + offline run (notebook exported to script, stdin piped, USE_LIVE_DATA=False): prompts,
  fuzzy matching ("slow down" → SlowDown, "imara daima" → ImaraDaima), snapshot fallback and KB> console all work.
- Search correctness: UCS and A* (scaled euclidean/manhattan/chebyshev) match networkx Dijkstra on all 702
  ordered pairs; unscaled heuristics produce 21/702 and 33/702 non-optimal routes (shown as the reason for scaling).
- Rule tests: 15/16 before the documented debugging fix (unknown obstacle), 16/16 after.
- Geo sanity check finds HillView (ambiguous name), Langata (vague centroid) and Practical 3's 0.5 km
  Lavington–J11–Kilimani segments (disputed lengths).
- Outputs depend on live weather; with no network the notebook uses the 2026-11-16 snapshot.
- Placeholder left for the user: group member names in the title cell.
