```yaml
  - name: Import Test dashboard
      community.grafana.grafana_dashboard:
        grafana_url: "http://192.168.50.33:3000"
        grafana_api_key: "{{ grafana_api }}"
        state: present
        commit_message: Updated by ansible
        overwrite: yes
        path: /vagrant/deployment/playbook/templates/dashboard/foo.json
```
Voici la commande Curl pour envoyer son dashboard : 
```bash
curl Command : curl -X POST http://192.168.50.33:3000/api/dashboards/db -u admin:adminpass -H "Content-Type: application/json" -H "accept: application/json" -d @filename
```