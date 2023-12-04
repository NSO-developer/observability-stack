.PHONY: help
help:
	@echo ""


.PHONY: start
start:
	docker compose up -d
	sleep 15
	$(MAKE) load-dashboards


.PHONY: stop
stop:
	docker compose stop

.PHONY: pull
pull:
	docker compose pull

.PHONY: clean
clean:
	docker run --rm -v $(PWD)/data:/data alpine sh -c 'rm -rf /data/*'

.PHONY: load-dashboards
load-dashboards:
	# Create folder
	curl -H "Content-Type: application/json" -X POST http://localhost:3000/api/folders --upload grafana/dashboards/folder.json
	./grafana-dashboard.py load --clean -f grafana/dashboards/node-exporter-full.json
	./grafana-dashboard.py load --clean -f grafana/dashboards/nso-log-files.json
	./grafana-dashboard.py load --clean -f grafana/dashboards/nso-metrics-exporter.json
	./grafana-dashboard.py load --clean -f grafana/dashboards/nso-observability-exporter-traces.json
	./grafana-dashboard.py load --clean -f grafana/dashboards/nso-observability-exporter.json
	./grafana-dashboard.py load --clean -f grafana/dashboards/nso-process-exporter.json
	./grafana-dashboard.py load --clean -f grafana/dashboards/nso-prometheus-process-exporter.json
