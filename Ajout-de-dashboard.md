Vous trouverez ci-dessous la manière de pousser un dashboard sur mesure depuis ansible. 
Cet exemple utilise un role, il serait donc interessant de le faire en interagissant seulement avec l'api de grafana
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


Notre dashboard custom : 
```json
{
  "annotations": {
    "list": [
      {
        "builtIn": 1,
        "datasource": "-- Grafana --",
        "enable": true,
        "hide": true,
        "iconColor": "rgba(0, 211, 255, 1)",
        "name": "Annotations & Alerts",
        "type": "dashboard"
      }
    ]
  },
  "editable": true,
  "gnetId": null,
  "graphTooltip": 0,
  "id": 45,
  "iteration": 1613836120171,
  "links": [],
  "panels": [
    {
      "collapsed": false,
      "datasource": null,
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 0
      },
      "id": 2,
      "panels": [],
      "title": "Overview",
      "type": "row"
    },
    {
      "datasource": null,
      "fieldConfig": {
        "defaults": {
          "color": {},
          "custom": {},
          "thresholds": {
            "mode": "absolute",
            "steps": []
          }
        },
        "overrides": []
      },
      "gridPos": {
        "h": 6,
        "w": 5,
        "x": 0,
        "y": 1
      },
      "id": 4,
      "options": {
        "content": "<h3 style=\"text-align:center;margin-top:20%; font-size:3em\">${server}</h3>",
        "mode": "html"
      },
      "pluginVersion": "7.4.0",
      "repeat": "server",
      "repeatDirection": "v",
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "devops-ansible",
          "value": "devops-ansible"
        }
      },
      "targets": [
        {
          "groupBy": [
            {
              "params": [
                "$__interval"
              ],
              "type": "time"
            },
            {
              "params": [
                "null"
              ],
              "type": "fill"
            }
          ],
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "time_series",
          "select": [
            [
              {
                "params": [
                  "value"
                ],
                "type": "field"
              },
              {
                "params": [],
                "type": "mean"
              }
            ]
          ],
          "tags": []
        }
      ],
      "timeFrom": null,
      "timeShift": null,
      "title": "",
      "type": "text"
    },
    {
      "datasource": null,
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "custom": {},
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              }
            ]
          },
          "unit": "s"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 6,
        "w": 6,
        "x": 5,
        "y": 1
      },
      "id": 8,
      "options": {
        "colorMode": "value",
        "graphMode": "area",
        "justifyMode": "auto",
        "orientation": "auto",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "/^last$/",
          "values": false
        },
        "text": {},
        "textMode": "auto"
      },
      "pluginVersion": "7.4.0",
      "repeat": "server",
      "repeatDirection": "v",
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "devops-ansible",
          "value": "devops-ansible"
        }
      },
      "targets": [
        {
          "groupBy": [],
          "measurement": "system",
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "table",
          "select": [
            [
              {
                "params": [
                  "uptime"
                ],
                "type": "field"
              },
              {
                "params": [],
                "type": "last"
              }
            ]
          ],
          "tags": [
            {
              "key": "host",
              "operator": "=~",
              "value": "/^$server$/"
            }
          ]
        }
      ],
      "title": "Uptime",
      "type": "stat"
    },
    {
      "datasource": null,
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "custom": {},
          "decimals": 1,
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              }
            ]
          },
          "unit": "percent"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 6,
        "w": 6,
        "x": 11,
        "y": 1
      },
      "id": 13,
      "options": {
        "colorMode": "value",
        "graphMode": "area",
        "justifyMode": "auto",
        "orientation": "auto",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "/^last$/",
          "values": false
        },
        "text": {},
        "textMode": "auto"
      },
      "pluginVersion": "7.4.0",
      "repeat": "server",
      "repeatDirection": "v",
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "devops-ansible",
          "value": "devops-ansible"
        }
      },
      "targets": [
        {
          "groupBy": [
            {
              "params": [
                "$interval"
              ],
              "type": "time"
            }
          ],
          "measurement": "cpu",
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "table",
          "select": [
            [
              {
                "params": [
                  "usage_system"
                ],
                "type": "field"
              },
              {
                "params": [],
                "type": "last"
              }
            ]
          ],
          "tags": [
            {
              "key": "host",
              "operator": "=~",
              "value": "/^$server$/"
            }
          ]
        }
      ],
      "title": "CPU Usage",
      "type": "stat"
    },
    {
      "datasource": null,
      "fieldConfig": {
        "defaults": {
          "color": {},
          "custom": {},
          "thresholds": {
            "mode": "absolute",
            "steps": []
          }
        },
        "overrides": []
      },
      "gridPos": {
        "h": 6,
        "w": 5,
        "x": 0,
        "y": 7
      },
      "id": 14,
      "options": {
        "content": "<h3 style=\"text-align:center;margin-top:20%; font-size:3em\">${server}</h3>",
        "mode": "html"
      },
      "pluginVersion": "7.4.0",
      "repeatDirection": "v",
      "repeatIteration": 1613836120171,
      "repeatPanelId": 4,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "devops-grafana",
          "value": "devops-grafana"
        }
      },
      "targets": [
        {
          "groupBy": [
            {
              "params": [
                "$__interval"
              ],
              "type": "time"
            },
            {
              "params": [
                "null"
              ],
              "type": "fill"
            }
          ],
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "time_series",
          "select": [
            [
              {
                "params": [
                  "value"
                ],
                "type": "field"
              },
              {
                "params": [],
                "type": "mean"
              }
            ]
          ],
          "tags": []
        }
      ],
      "timeFrom": null,
      "timeShift": null,
      "title": "",
      "type": "text"
    },
    {
      "datasource": null,
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "custom": {},
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              }
            ]
          },
          "unit": "s"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 6,
        "w": 6,
        "x": 5,
        "y": 7
      },
      "id": 16,
      "options": {
        "colorMode": "value",
        "graphMode": "area",
        "justifyMode": "auto",
        "orientation": "auto",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "/^last$/",
          "values": false
        },
        "text": {},
        "textMode": "auto"
      },
      "pluginVersion": "7.4.0",
      "repeatDirection": "v",
      "repeatIteration": 1613836120171,
      "repeatPanelId": 8,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "devops-grafana",
          "value": "devops-grafana"
        }
      },
      "targets": [
        {
          "groupBy": [],
          "measurement": "system",
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "table",
          "select": [
            [
              {
                "params": [
                  "uptime"
                ],
                "type": "field"
              },
              {
                "params": [],
                "type": "last"
              }
            ]
          ],
          "tags": [
            {
              "key": "host",
              "operator": "=~",
              "value": "/^$server$/"
            }
          ]
        }
      ],
      "title": "Uptime",
      "type": "stat"
    },
    {
      "datasource": null,
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "custom": {},
          "decimals": 1,
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              }
            ]
          },
          "unit": "percent"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 6,
        "w": 6,
        "x": 11,
        "y": 7
      },
      "id": 18,
      "options": {
        "colorMode": "value",
        "graphMode": "area",
        "justifyMode": "auto",
        "orientation": "auto",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "/^last$/",
          "values": false
        },
        "text": {},
        "textMode": "auto"
      },
      "pluginVersion": "7.4.0",
      "repeatDirection": "v",
      "repeatIteration": 1613836120171,
      "repeatPanelId": 13,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "devops-grafana",
          "value": "devops-grafana"
        }
      },
      "targets": [
        {
          "groupBy": [
            {
              "params": [
                "$interval"
              ],
              "type": "time"
            }
          ],
          "measurement": "cpu",
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "table",
          "select": [
            [
              {
                "params": [
                  "usage_system"
                ],
                "type": "field"
              },
              {
                "params": [],
                "type": "last"
              }
            ]
          ],
          "tags": [
            {
              "key": "host",
              "operator": "=~",
              "value": "/^$server$/"
            }
          ]
        }
      ],
      "title": "CPU Usage",
      "type": "stat"
    },
    {
      "datasource": null,
      "fieldConfig": {
        "defaults": {
          "color": {},
          "custom": {},
          "thresholds": {
            "mode": "absolute",
            "steps": []
          }
        },
        "overrides": []
      },
      "gridPos": {
        "h": 6,
        "w": 5,
        "x": 0,
        "y": 13
      },
      "id": 15,
      "options": {
        "content": "<h3 style=\"text-align:center;margin-top:20%; font-size:3em\">${server}</h3>",
        "mode": "html"
      },
      "pluginVersion": "7.4.0",
      "repeatDirection": "v",
      "repeatIteration": 1613836120171,
      "repeatPanelId": 4,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "devops-influxdb",
          "value": "devops-influxdb"
        }
      },
      "targets": [
        {
          "groupBy": [
            {
              "params": [
                "$__interval"
              ],
              "type": "time"
            },
            {
              "params": [
                "null"
              ],
              "type": "fill"
            }
          ],
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "time_series",
          "select": [
            [
              {
                "params": [
                  "value"
                ],
                "type": "field"
              },
              {
                "params": [],
                "type": "mean"
              }
            ]
          ],
          "tags": []
        }
      ],
      "timeFrom": null,
      "timeShift": null,
      "title": "",
      "type": "text"
    },
    {
      "datasource": null,
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "custom": {},
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              }
            ]
          },
          "unit": "s"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 6,
        "w": 6,
        "x": 5,
        "y": 13
      },
      "id": 17,
      "options": {
        "colorMode": "value",
        "graphMode": "area",
        "justifyMode": "auto",
        "orientation": "auto",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "/^last$/",
          "values": false
        },
        "text": {},
        "textMode": "auto"
      },
      "pluginVersion": "7.4.0",
      "repeatDirection": "v",
      "repeatIteration": 1613836120171,
      "repeatPanelId": 8,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "devops-influxdb",
          "value": "devops-influxdb"
        }
      },
      "targets": [
        {
          "groupBy": [],
          "measurement": "system",
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "table",
          "select": [
            [
              {
                "params": [
                  "uptime"
                ],
                "type": "field"
              },
              {
                "params": [],
                "type": "last"
              }
            ]
          ],
          "tags": [
            {
              "key": "host",
              "operator": "=~",
              "value": "/^$server$/"
            }
          ]
        }
      ],
      "title": "Uptime",
      "type": "stat"
    },
    {
      "datasource": null,
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "custom": {},
          "decimals": 1,
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              }
            ]
          },
          "unit": "percent"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 6,
        "w": 6,
        "x": 11,
        "y": 13
      },
      "id": 19,
      "options": {
        "colorMode": "value",
        "graphMode": "area",
        "justifyMode": "auto",
        "orientation": "auto",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "/^last$/",
          "values": false
        },
        "text": {},
        "textMode": "auto"
      },
      "pluginVersion": "7.4.0",
      "repeatDirection": "v",
      "repeatIteration": 1613836120171,
      "repeatPanelId": 13,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "devops-influxdb",
          "value": "devops-influxdb"
        }
      },
      "targets": [
        {
          "groupBy": [
            {
              "params": [
                "$interval"
              ],
              "type": "time"
            }
          ],
          "measurement": "cpu",
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "table",
          "select": [
            [
              {
                "params": [
                  "usage_system"
                ],
                "type": "field"
              },
              {
                "params": [],
                "type": "last"
              }
            ]
          ],
          "tags": [
            {
              "key": "host",
              "operator": "=~",
              "value": "/^$server$/"
            }
          ]
        }
      ],
      "title": "CPU Usage",
      "type": "stat"
    }
  ],
  "refresh": false,
  "schemaVersion": 27,
  "style": "dark",
  "tags": [],
  "templating": {
    "list": [
      {
        "allValue": null,
        "current": {
          "selected": false,
          "text": "project_local",
          "value": "project_local"
        },
        "description": null,
        "error": null,
        "hide": 2,
        "includeAll": false,
        "label": "Project",
        "multi": false,
        "name": "project",
        "options": [
          {
            "selected": true,
            "text": "project_local",
            "value": "project_local"
          }
        ],
        "query": "project_local",
        "skipUrlSync": false,
        "type": "custom"
      },
      {
        "allValue": ".*",
        "current": {
          "selected": false,
          "text": [
            "All"
          ],
          "value": [
            "$__all"
          ]
        },
        "datasource": null,
        "definition": "SHOW TAG VALUES WITH KEY = \"host\" WHERE \"projet\" =~ /$project/",
        "description": null,
        "error": null,
        "hide": 0,
        "includeAll": true,
        "label": "Server",
        "multi": true,
        "name": "server",
        "options": [],
        "query": "SHOW TAG VALUES WITH KEY = \"host\" WHERE \"projet\" =~ /$project/",
        "refresh": 1,
        "regex": "",
        "skipUrlSync": false,
        "sort": 0,
        "tagValuesQuery": "",
        "tags": [],
        "tagsQuery": "",
        "type": "query",
        "useTags": false
      }
    ]
  },
  "time": {
    "from": "now-15m",
    "to": "now"
  },
  "timepicker": {},
  "timezone": "",
  "title": "COnfig manuelle",
  "uid": "3Xoy8isMk",
  "version": 6
}
```