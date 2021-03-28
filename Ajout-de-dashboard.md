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
        "limit": 100,
        "name": "Annotations & Alerts",
        "showIn": 0,
        "type": "dashboard"
      }
    ]
  },
  "editable": true,
  "gnetId": null,
  "graphTooltip": 0,
  "id": 4,
  "iteration": 1616889901871,
  "links": [],
  "panels": [
    {
      "datasource": null,
      "fieldConfig": {
        "defaults": {
          "custom": {}
        },
        "overrides": []
      },
      "gridPos": {
        "h": 3,
        "w": 19,
        "x": 0,
        "y": 0
      },
      "id": 146,
      "options": {
        "content": "<h3 style=\"text-align:center; margin-top: 1%; font-size:4em\">${project}</h3>",
        "mode": "markdown"
      },
      "pluginVersion": "7.4.3",
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
          "custom": {}
        },
        "overrides": []
      },
      "gridPos": {
        "h": 3,
        "w": 5,
        "x": 19,
        "y": 0
      },
      "id": 170,
      "options": {
        "bgColor": "rgba(25, 25, 25, 0.63)",
        "clockType": "24 hour",
        "countdownSettings": {
          "endCountdownTime": "2021-03-07T00:58:26+01:00",
          "endText": "00:00:00"
        },
        "dateSettings": {
          "dateFormat": "YYYY-MM-DD",
          "fontSize": "20px",
          "fontWeight": "normal",
          "showDate": false
        },
        "mode": "time",
        "timeSettings": {
          "fontSize": "50px",
          "fontWeight": "normal"
        },
        "timezone": "Europe/Paris",
        "timezoneSettings": {
          "fontSize": "12px",
          "fontWeight": "normal",
          "showTimezone": false,
          "zoneFormat": "offsetAbbv"
        }
      },
      "pluginVersion": "7.4.3",
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
      "title": "Heure",
      "type": "grafana-clock-panel"
    },
    {
      "collapsed": false,
      "datasource": null,
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 3
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
        "h": 2,
        "w": 3,
        "x": 0,
        "y": 4
      },
      "id": 4,
      "options": {
        "content": "<h3 style=\"text-align:center; margin-top: 10%; font-size:1.5em\">${server}</h3>",
        "mode": "html"
      },
      "pluginVersion": "7.4.3",
      "repeat": "server",
      "repeatDirection": "v",
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "ansible.monitoring.devops.ydays.ynov.fr",
          "value": "ansible.monitoring.devops.ydays.ynov.fr"
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
          "unit": "s"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 2,
        "w": 2,
        "x": 3,
        "y": 4
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
      "pluginVersion": "7.4.3",
      "repeat": "server",
      "repeatDirection": "v",
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "ansible.monitoring.devops.ydays.ynov.fr",
          "value": "ansible.monitoring.devops.ydays.ynov.fr"
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
              },
              {
                "color": "#EAB839",
                "value": 70
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "percent"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 2,
        "w": 4,
        "x": 5,
        "y": 4
      },
      "id": 13,
      "options": {
        "displayMode": "lcd",
        "orientation": "horizontal",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "/^last$/",
          "values": false
        },
        "showUnfilled": true,
        "text": {}
      },
      "pluginVersion": "7.4.3",
      "repeat": "server",
      "repeatDirection": "v",
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "ansible.monitoring.devops.ydays.ynov.fr",
          "value": "ansible.monitoring.devops.ydays.ynov.fr"
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
          "query": "SELECT last(\"usage_idle\") FROM \"cpu\" WHERE (\"host\" =~ /^$server$/) AND $timeFilter GROUP BY time($interval)",
          "rawQuery": false,
          "refId": "A",
          "resultFormat": "table",
          "select": [
            [
              {
                "params": [
                  "usage_idle"
                ],
                "type": "field"
              },
              {
                "params": [],
                "type": "last"
              },
              {
                "params": [
                  " *-1 + 100"
                ],
                "type": "math"
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
      "type": "bargauge"
    },
    {
      "datasource": null,
      "description": "",
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "custom": {},
          "mappings": [],
          "thresholds": {
            "mode": "percentage",
            "steps": [
              {
                "color": "green",
                "value": null
              },
              {
                "color": "#EAB839",
                "value": 70
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "percent"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 2,
        "w": 4,
        "x": 9,
        "y": 4
      },
      "id": 21,
      "options": {
        "displayMode": "lcd",
        "orientation": "horizontal",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "",
          "values": false
        },
        "showUnfilled": true,
        "text": {}
      },
      "pluginVersion": "7.4.3",
      "repeat": "server",
      "repeatDirection": "v",
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "ansible.monitoring.devops.ydays.ynov.fr",
          "value": "ansible.monitoring.devops.ydays.ynov.fr"
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
          "measurement": "mem",
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "time_series",
          "select": [
            [
              {
                "params": [
                  "used_percent"
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
      "timeFrom": null,
      "timeShift": null,
      "title": "Memory Use",
      "type": "bargauge"
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
              },
              {
                "color": "#EAB839",
                "value": 70
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "percent"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 2,
        "w": 4,
        "x": 13,
        "y": 4
      },
      "id": 31,
      "options": {
        "displayMode": "lcd",
        "orientation": "horizontal",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "",
          "values": false
        },
        "showUnfilled": true,
        "text": {}
      },
      "pluginVersion": "7.4.3",
      "repeat": "server",
      "repeatDirection": "v",
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "ansible.monitoring.devops.ydays.ynov.fr",
          "value": "ansible.monitoring.devops.ydays.ynov.fr"
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
          "measurement": "disk",
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "time_series",
          "select": [
            [
              {
                "params": [
                  "used_percent"
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
            },
            {
              "condition": "AND",
              "key": "path",
              "operator": "=",
              "value": "/"
            }
          ]
        }
      ],
      "timeFrom": null,
      "timeShift": null,
      "title": "Disk Use $server",
      "type": "bargauge"
    },
    {
      "datasource": null,
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "custom": {},
          "decimals": 2,
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              },
              {
                "color": "#EAB839",
                "value": 60
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "percent"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 2,
        "w": 4,
        "x": 17,
        "y": 4
      },
      "id": 122,
      "options": {
        "displayMode": "lcd",
        "orientation": "horizontal",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "",
          "values": false
        },
        "showUnfilled": true,
        "text": {}
      },
      "pluginVersion": "7.4.3",
      "repeat": "server",
      "repeatDirection": "v",
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "ansible.monitoring.devops.ydays.ynov.fr",
          "value": "ansible.monitoring.devops.ydays.ynov.fr"
        }
      },
      "targets": [
        {
          "groupBy": [],
          "measurement": "swap",
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "time_series",
          "select": [
            [
              {
                "params": [
                  "used_percent"
                ],
                "type": "field"
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
      "title": "SWAP utilisée",
      "type": "bargauge"
    },
    {
      "cacheTimeout": null,
      "colorBackground": false,
      "colorValue": true,
      "colors": [
        "rgba(50, 172, 45, 0.97)",
        "rgba(237, 129, 40, 0.89)",
        "rgba(245, 54, 54, 0.9)"
      ],
      "datasource": null,
      "decimals": 0,
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {}
        },
        "overrides": []
      },
      "format": "none",
      "gauge": {
        "maxValue": 100,
        "minValue": 0,
        "show": false,
        "thresholdLabels": false,
        "thresholdMarkers": true
      },
      "gridPos": {
        "h": 2,
        "w": 3,
        "x": 21,
        "y": 4
      },
      "height": "150",
      "id": 35,
      "interval": null,
      "links": [],
      "mappingType": 1,
      "mappingTypes": [
        {
          "name": "value to text",
          "value": 1
        },
        {
          "name": "range to text",
          "value": 2
        }
      ],
      "maxDataPoints": 100,
      "nullPointMode": "connected",
      "nullText": null,
      "postfix": "",
      "postfixFontSize": "50%",
      "prefix": "",
      "prefixFontSize": "50%",
      "rangeMaps": [
        {
          "from": "null",
          "text": "N/A",
          "to": "null"
        }
      ],
      "repeat": "server",
      "repeatDirection": "v",
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "ansible.monitoring.devops.ydays.ynov.fr",
          "value": "ansible.monitoring.devops.ydays.ynov.fr"
        }
      },
      "sparkline": {
        "fillColor": "rgba(31, 118, 189, 0.18)",
        "full": false,
        "lineColor": "rgb(31, 120, 193)",
        "show": true
      },
      "tableColumn": "",
      "targets": [
        {
          "dsType": "influxdb",
          "groupBy": [],
          "measurement": "processes",
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "time_series",
          "select": [
            [
              {
                "params": [
                  "total"
                ],
                "type": "field"
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
      "thresholds": "1,5,10",
      "title": "Processes",
      "type": "singlestat",
      "valueFontSize": "80%",
      "valueMaps": [
        {
          "op": "=",
          "text": "N/A",
          "value": "null"
        }
      ],
      "valueName": "current"
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
        "h": 2,
        "w": 3,
        "x": 0,
        "y": 6
      },
      "id": 428,
      "options": {
        "content": "<h3 style=\"text-align:center; margin-top: 10%; font-size:1.5em\">${server}</h3>",
        "mode": "html"
      },
      "pluginVersion": "7.4.3",
      "repeatDirection": "v",
      "repeatIteration": 1616889901871,
      "repeatPanelId": 4,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "grafana.monitoring.devops.ydays.ynov.fr",
          "value": "grafana.monitoring.devops.ydays.ynov.fr"
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
          "unit": "s"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 2,
        "w": 2,
        "x": 3,
        "y": 6
      },
      "id": 430,
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
      "pluginVersion": "7.4.3",
      "repeatDirection": "v",
      "repeatIteration": 1616889901871,
      "repeatPanelId": 8,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "grafana.monitoring.devops.ydays.ynov.fr",
          "value": "grafana.monitoring.devops.ydays.ynov.fr"
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
              },
              {
                "color": "#EAB839",
                "value": 70
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "percent"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 2,
        "w": 4,
        "x": 5,
        "y": 6
      },
      "id": 432,
      "options": {
        "displayMode": "lcd",
        "orientation": "horizontal",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "/^last$/",
          "values": false
        },
        "showUnfilled": true,
        "text": {}
      },
      "pluginVersion": "7.4.3",
      "repeatDirection": "v",
      "repeatIteration": 1616889901871,
      "repeatPanelId": 13,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "grafana.monitoring.devops.ydays.ynov.fr",
          "value": "grafana.monitoring.devops.ydays.ynov.fr"
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
          "query": "SELECT last(\"usage_idle\") FROM \"cpu\" WHERE (\"host\" =~ /^$server$/) AND $timeFilter GROUP BY time($interval)",
          "rawQuery": false,
          "refId": "A",
          "resultFormat": "table",
          "select": [
            [
              {
                "params": [
                  "usage_idle"
                ],
                "type": "field"
              },
              {
                "params": [],
                "type": "last"
              },
              {
                "params": [
                  " *-1 + 100"
                ],
                "type": "math"
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
      "type": "bargauge"
    },
    {
      "datasource": null,
      "description": "",
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "custom": {},
          "mappings": [],
          "thresholds": {
            "mode": "percentage",
            "steps": [
              {
                "color": "green",
                "value": null
              },
              {
                "color": "#EAB839",
                "value": 70
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "percent"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 2,
        "w": 4,
        "x": 9,
        "y": 6
      },
      "id": 434,
      "options": {
        "displayMode": "lcd",
        "orientation": "horizontal",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "",
          "values": false
        },
        "showUnfilled": true,
        "text": {}
      },
      "pluginVersion": "7.4.3",
      "repeatDirection": "v",
      "repeatIteration": 1616889901871,
      "repeatPanelId": 21,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "grafana.monitoring.devops.ydays.ynov.fr",
          "value": "grafana.monitoring.devops.ydays.ynov.fr"
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
          "measurement": "mem",
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "time_series",
          "select": [
            [
              {
                "params": [
                  "used_percent"
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
      "timeFrom": null,
      "timeShift": null,
      "title": "Memory Use",
      "type": "bargauge"
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
              },
              {
                "color": "#EAB839",
                "value": 70
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "percent"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 2,
        "w": 4,
        "x": 13,
        "y": 6
      },
      "id": 436,
      "options": {
        "displayMode": "lcd",
        "orientation": "horizontal",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "",
          "values": false
        },
        "showUnfilled": true,
        "text": {}
      },
      "pluginVersion": "7.4.3",
      "repeatDirection": "v",
      "repeatIteration": 1616889901871,
      "repeatPanelId": 31,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "grafana.monitoring.devops.ydays.ynov.fr",
          "value": "grafana.monitoring.devops.ydays.ynov.fr"
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
          "measurement": "disk",
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "time_series",
          "select": [
            [
              {
                "params": [
                  "used_percent"
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
            },
            {
              "condition": "AND",
              "key": "path",
              "operator": "=",
              "value": "/"
            }
          ]
        }
      ],
      "timeFrom": null,
      "timeShift": null,
      "title": "Disk Use $server",
      "type": "bargauge"
    },
    {
      "datasource": null,
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "custom": {},
          "decimals": 2,
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              },
              {
                "color": "#EAB839",
                "value": 60
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "percent"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 2,
        "w": 4,
        "x": 17,
        "y": 6
      },
      "id": 438,
      "options": {
        "displayMode": "lcd",
        "orientation": "horizontal",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "",
          "values": false
        },
        "showUnfilled": true,
        "text": {}
      },
      "pluginVersion": "7.4.3",
      "repeatDirection": "v",
      "repeatIteration": 1616889901871,
      "repeatPanelId": 122,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "grafana.monitoring.devops.ydays.ynov.fr",
          "value": "grafana.monitoring.devops.ydays.ynov.fr"
        }
      },
      "targets": [
        {
          "groupBy": [],
          "measurement": "swap",
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "time_series",
          "select": [
            [
              {
                "params": [
                  "used_percent"
                ],
                "type": "field"
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
      "title": "SWAP utilisée",
      "type": "bargauge"
    },
    {
      "cacheTimeout": null,
      "colorBackground": false,
      "colorValue": true,
      "colors": [
        "rgba(50, 172, 45, 0.97)",
        "rgba(237, 129, 40, 0.89)",
        "rgba(245, 54, 54, 0.9)"
      ],
      "datasource": null,
      "decimals": 0,
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {}
        },
        "overrides": []
      },
      "format": "none",
      "gauge": {
        "maxValue": 100,
        "minValue": 0,
        "show": false,
        "thresholdLabels": false,
        "thresholdMarkers": true
      },
      "gridPos": {
        "h": 2,
        "w": 3,
        "x": 21,
        "y": 6
      },
      "height": "150",
      "id": 440,
      "interval": null,
      "links": [],
      "mappingType": 1,
      "mappingTypes": [
        {
          "name": "value to text",
          "value": 1
        },
        {
          "name": "range to text",
          "value": 2
        }
      ],
      "maxDataPoints": 100,
      "nullPointMode": "connected",
      "nullText": null,
      "postfix": "",
      "postfixFontSize": "50%",
      "prefix": "",
      "prefixFontSize": "50%",
      "rangeMaps": [
        {
          "from": "null",
          "text": "N/A",
          "to": "null"
        }
      ],
      "repeatDirection": "v",
      "repeatIteration": 1616889901871,
      "repeatPanelId": 35,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "grafana.monitoring.devops.ydays.ynov.fr",
          "value": "grafana.monitoring.devops.ydays.ynov.fr"
        }
      },
      "sparkline": {
        "fillColor": "rgba(31, 118, 189, 0.18)",
        "full": false,
        "lineColor": "rgb(31, 120, 193)",
        "show": true
      },
      "tableColumn": "",
      "targets": [
        {
          "dsType": "influxdb",
          "groupBy": [],
          "measurement": "processes",
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "time_series",
          "select": [
            [
              {
                "params": [
                  "total"
                ],
                "type": "field"
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
      "thresholds": "1,5,10",
      "title": "Processes",
      "type": "singlestat",
      "valueFontSize": "80%",
      "valueMaps": [
        {
          "op": "=",
          "text": "N/A",
          "value": "null"
        }
      ],
      "valueName": "current"
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
        "h": 2,
        "w": 3,
        "x": 0,
        "y": 8
      },
      "id": 429,
      "options": {
        "content": "<h3 style=\"text-align:center; margin-top: 10%; font-size:1.5em\">${server}</h3>",
        "mode": "html"
      },
      "pluginVersion": "7.4.3",
      "repeatDirection": "v",
      "repeatIteration": 1616889901871,
      "repeatPanelId": 4,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "influxdb.monitoring.devops.ydays.ynov.fr",
          "value": "influxdb.monitoring.devops.ydays.ynov.fr"
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
          "unit": "s"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 2,
        "w": 2,
        "x": 3,
        "y": 8
      },
      "id": 431,
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
      "pluginVersion": "7.4.3",
      "repeatDirection": "v",
      "repeatIteration": 1616889901871,
      "repeatPanelId": 8,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "influxdb.monitoring.devops.ydays.ynov.fr",
          "value": "influxdb.monitoring.devops.ydays.ynov.fr"
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
              },
              {
                "color": "#EAB839",
                "value": 70
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "percent"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 2,
        "w": 4,
        "x": 5,
        "y": 8
      },
      "id": 433,
      "options": {
        "displayMode": "lcd",
        "orientation": "horizontal",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "/^last$/",
          "values": false
        },
        "showUnfilled": true,
        "text": {}
      },
      "pluginVersion": "7.4.3",
      "repeatDirection": "v",
      "repeatIteration": 1616889901871,
      "repeatPanelId": 13,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "influxdb.monitoring.devops.ydays.ynov.fr",
          "value": "influxdb.monitoring.devops.ydays.ynov.fr"
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
          "query": "SELECT last(\"usage_idle\") FROM \"cpu\" WHERE (\"host\" =~ /^$server$/) AND $timeFilter GROUP BY time($interval)",
          "rawQuery": false,
          "refId": "A",
          "resultFormat": "table",
          "select": [
            [
              {
                "params": [
                  "usage_idle"
                ],
                "type": "field"
              },
              {
                "params": [],
                "type": "last"
              },
              {
                "params": [
                  " *-1 + 100"
                ],
                "type": "math"
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
      "type": "bargauge"
    },
    {
      "datasource": null,
      "description": "",
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "custom": {},
          "mappings": [],
          "thresholds": {
            "mode": "percentage",
            "steps": [
              {
                "color": "green",
                "value": null
              },
              {
                "color": "#EAB839",
                "value": 70
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "percent"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 2,
        "w": 4,
        "x": 9,
        "y": 8
      },
      "id": 435,
      "options": {
        "displayMode": "lcd",
        "orientation": "horizontal",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "",
          "values": false
        },
        "showUnfilled": true,
        "text": {}
      },
      "pluginVersion": "7.4.3",
      "repeatDirection": "v",
      "repeatIteration": 1616889901871,
      "repeatPanelId": 21,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "influxdb.monitoring.devops.ydays.ynov.fr",
          "value": "influxdb.monitoring.devops.ydays.ynov.fr"
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
          "measurement": "mem",
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "time_series",
          "select": [
            [
              {
                "params": [
                  "used_percent"
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
      "timeFrom": null,
      "timeShift": null,
      "title": "Memory Use",
      "type": "bargauge"
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
              },
              {
                "color": "#EAB839",
                "value": 70
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "percent"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 2,
        "w": 4,
        "x": 13,
        "y": 8
      },
      "id": 437,
      "options": {
        "displayMode": "lcd",
        "orientation": "horizontal",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "",
          "values": false
        },
        "showUnfilled": true,
        "text": {}
      },
      "pluginVersion": "7.4.3",
      "repeatDirection": "v",
      "repeatIteration": 1616889901871,
      "repeatPanelId": 31,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "influxdb.monitoring.devops.ydays.ynov.fr",
          "value": "influxdb.monitoring.devops.ydays.ynov.fr"
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
          "measurement": "disk",
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "time_series",
          "select": [
            [
              {
                "params": [
                  "used_percent"
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
            },
            {
              "condition": "AND",
              "key": "path",
              "operator": "=",
              "value": "/"
            }
          ]
        }
      ],
      "timeFrom": null,
      "timeShift": null,
      "title": "Disk Use $server",
      "type": "bargauge"
    },
    {
      "datasource": null,
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "custom": {},
          "decimals": 2,
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              },
              {
                "color": "#EAB839",
                "value": 60
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "percent"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 2,
        "w": 4,
        "x": 17,
        "y": 8
      },
      "id": 439,
      "options": {
        "displayMode": "lcd",
        "orientation": "horizontal",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "",
          "values": false
        },
        "showUnfilled": true,
        "text": {}
      },
      "pluginVersion": "7.4.3",
      "repeatDirection": "v",
      "repeatIteration": 1616889901871,
      "repeatPanelId": 122,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "influxdb.monitoring.devops.ydays.ynov.fr",
          "value": "influxdb.monitoring.devops.ydays.ynov.fr"
        }
      },
      "targets": [
        {
          "groupBy": [],
          "measurement": "swap",
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "time_series",
          "select": [
            [
              {
                "params": [
                  "used_percent"
                ],
                "type": "field"
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
      "title": "SWAP utilisée",
      "type": "bargauge"
    },
    {
      "cacheTimeout": null,
      "colorBackground": false,
      "colorValue": true,
      "colors": [
        "rgba(50, 172, 45, 0.97)",
        "rgba(237, 129, 40, 0.89)",
        "rgba(245, 54, 54, 0.9)"
      ],
      "datasource": null,
      "decimals": 0,
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {}
        },
        "overrides": []
      },
      "format": "none",
      "gauge": {
        "maxValue": 100,
        "minValue": 0,
        "show": false,
        "thresholdLabels": false,
        "thresholdMarkers": true
      },
      "gridPos": {
        "h": 2,
        "w": 3,
        "x": 21,
        "y": 8
      },
      "height": "150",
      "id": 441,
      "interval": null,
      "links": [],
      "mappingType": 1,
      "mappingTypes": [
        {
          "name": "value to text",
          "value": 1
        },
        {
          "name": "range to text",
          "value": 2
        }
      ],
      "maxDataPoints": 100,
      "nullPointMode": "connected",
      "nullText": null,
      "postfix": "",
      "postfixFontSize": "50%",
      "prefix": "",
      "prefixFontSize": "50%",
      "rangeMaps": [
        {
          "from": "null",
          "text": "N/A",
          "to": "null"
        }
      ],
      "repeatDirection": "v",
      "repeatIteration": 1616889901871,
      "repeatPanelId": 35,
      "scopedVars": {
        "server": {
          "selected": false,
          "text": "influxdb.monitoring.devops.ydays.ynov.fr",
          "value": "influxdb.monitoring.devops.ydays.ynov.fr"
        }
      },
      "sparkline": {
        "fillColor": "rgba(31, 118, 189, 0.18)",
        "full": false,
        "lineColor": "rgb(31, 120, 193)",
        "show": true
      },
      "tableColumn": "",
      "targets": [
        {
          "dsType": "influxdb",
          "groupBy": [],
          "measurement": "processes",
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
          "resultFormat": "time_series",
          "select": [
            [
              {
                "params": [
                  "total"
                ],
                "type": "field"
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
      "thresholds": "1,5,10",
      "title": "Processes",
      "type": "singlestat",
      "valueFontSize": "80%",
      "valueMaps": [
        {
          "op": "=",
          "text": "N/A",
          "value": "null"
        }
      ],
      "valueName": "current"
    },
    {
      "collapsed": true,
      "datasource": null,
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 10
      },
      "id": 194,
      "panels": [
        {
          "aliasColors": {},
          "bars": false,
          "dashLength": 10,
          "dashes": false,
          "datasource": null,
          "fieldConfig": {
            "defaults": {
              "custom": {}
            },
            "overrides": []
          },
          "fill": 1,
          "fillGradient": 0,
          "gridPos": {
            "h": 8,
            "w": 24,
            "x": 0,
            "y": 11
          },
          "hiddenSeries": false,
          "id": 379,
          "legend": {
            "alignAsTable": true,
            "avg": true,
            "current": true,
            "max": false,
            "min": true,
            "show": true,
            "total": false,
            "values": true
          },
          "lines": true,
          "linewidth": 1,
          "nullPointMode": "null",
          "options": {
            "alertThreshold": true
          },
          "percentage": false,
          "pluginVersion": "7.4.3",
          "pointradius": 2,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [
            {
              "$$hashKey": "object:1301",
              "alias": "/read/",
              "transform": "negative-Y"
            }
          ],
          "spaceLength": 10,
          "stack": false,
          "steppedLine": false,
          "targets": [
            {
              "alias": "$tag_host: $tag_name: $col",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                }
              ],
              "hide": true,
              "measurement": "diskio",
              "orderByTime": "ASC",
              "policy": "default",
              "query": "SELECT non_negative_derivative(mean(\"read_bytes\"), 1s) AS \"read\" FROM \"diskio\" WHERE (\"host\" =~ /^$server$/ AND \"projet\" =~ /^$project$/ AND \"name\" =~ /sda/ AND \"time\" > now() - 4w) GROUP BY time($__interval), \"host\", *",
              "rawQuery": true,
              "refId": "A",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "read_bytes"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  },
                  {
                    "params": [
                      "1s"
                    ],
                    "type": "non_negative_derivative"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": ">",
                  "value": "now() - 4w"
                }
              ]
            },
            {
              "alias": "$tag_host: $tag_name: $col",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "*"
                  ],
                  "type": "tag"
                }
              ],
              "hide": true,
              "measurement": "diskio",
              "orderByTime": "ASC",
              "policy": "default",
              "query": "SELECT non_negative_derivative(mean(\"write_bytes\"), 1s) AS \"write\" FROM \"diskio\" WHERE (\"host\" =~ /^$server$/ AND \"projet\" =~ /^$project$/ AND \"name\" =~ /sda/ AND \"time\" > now() - 4w) GROUP BY time($__interval), \"host\", *",
              "rawQuery": true,
              "refId": "B",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "read_bytes"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  },
                  {
                    "params": [
                      "1s"
                    ],
                    "type": "non_negative_derivative"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": ">",
                  "value": "now() - 4w"
                }
              ]
            },
            {
              "alias": "$tag_host: $tag_name: $col",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "*"
                  ],
                  "type": "tag"
                }
              ],
              "hide": true,
              "measurement": "diskio",
              "orderByTime": "ASC",
              "policy": "RP3month",
              "query": "SELECT non_negative_derivative(mean(\"mean_read_bytes\"), 1s) AS \"read\" FROM \"RP3month\".\"diskio\" WHERE (\"host\" =~ /^$server$/ AND \"projet\" =~ /^$project$/ AND \"name\" =~ /sda/ AND \"time\" < now() - 4w AND \"time\" > now() - 12w) GROUP BY time($__interval), *",
              "rawQuery": true,
              "refId": "C",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "mean_read_bytes"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  },
                  {
                    "params": [
                      "1s"
                    ],
                    "type": "non_negative_derivative"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": "<",
                  "value": "now() - 4w"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": ">",
                  "value": "now() - 12w"
                }
              ]
            },
            {
              "alias": "$tag_host: $tag_name: $col",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "*"
                  ],
                  "type": "tag"
                }
              ],
              "hide": true,
              "measurement": "diskio",
              "orderByTime": "ASC",
              "policy": "RP3month",
              "query": "SELECT non_negative_derivative(mean(\"mean_write_bytes\"), 1s) AS \"write\" FROM \"RP3month\".\"diskio\" WHERE (\"host\" =~ /^$server$/ AND \"projet\" =~ /^$project$/ AND \"name\" =~ /sda/ AND \"time\" < now() - 4w AND \"time\" > now() - 12w) GROUP BY time($__interval), *",
              "rawQuery": true,
              "refId": "D",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "mean_read_bytes"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  },
                  {
                    "params": [
                      "1s"
                    ],
                    "type": "non_negative_derivative"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": "<",
                  "value": "now() - 4w"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": ">",
                  "value": "now() - 12w"
                }
              ]
            },
            {
              "alias": "$tag_host: $tag_name: $col",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "*"
                  ],
                  "type": "tag"
                }
              ],
              "hide": true,
              "measurement": "diskio",
              "orderByTime": "ASC",
              "policy": "RP3month",
              "query": "SELECT non_negative_derivative(mean(\"mean_mean_read_bytes\"), 1s) AS \"read\" FROM \"RP6month\".\"diskio\" WHERE (\"host\" =~ /^$server$/ AND \"projet\" =~ /^$project$/ AND \"name\" =~ /sda/ AND \"time\" < now() - 12w) GROUP BY time($__interval), *",
              "rawQuery": true,
              "refId": "E",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "mean_read_bytes"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  },
                  {
                    "params": [
                      "1s"
                    ],
                    "type": "non_negative_derivative"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": "<",
                  "value": "now() - 4w"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": ">",
                  "value": "now() - 12w"
                }
              ]
            },
            {
              "alias": "$tag_host: $tag_name: $col",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "*"
                  ],
                  "type": "tag"
                }
              ],
              "hide": true,
              "measurement": "diskio",
              "orderByTime": "ASC",
              "policy": "RP3month",
              "query": "SELECT non_negative_derivative(mean(\"mean_mean_write_bytes\"), 1s) AS \"write\" FROM \"RP6month\".\"diskio\" WHERE (\"host\" =~ /^$server$/ AND \"projet\" =~ /^$project$/ AND \"name\" =~ /sda/ AND \"time\" < now() - 12w) GROUP BY time($__interval), *",
              "rawQuery": true,
              "refId": "F",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "mean_read_bytes"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  },
                  {
                    "params": [
                      "1s"
                    ],
                    "type": "non_negative_derivative"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": "<",
                  "value": "now() - 4w"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": ">",
                  "value": "now() - 12w"
                }
              ]
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeRegions": [],
          "timeShift": null,
          "title": "Lecture / Ecriture IO",
          "tooltip": {
            "shared": true,
            "sort": 0,
            "value_type": "individual"
          },
          "type": "graph",
          "xaxis": {
            "buckets": null,
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "$$hashKey": "object:1203",
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            },
            {
              "$$hashKey": "object:1204",
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ],
          "yaxis": {
            "align": false,
            "alignLevel": null
          }
        },
        {
          "aliasColors": {},
          "bars": false,
          "dashLength": 10,
          "dashes": false,
          "datasource": null,
          "fieldConfig": {
            "defaults": {
              "color": {},
              "custom": {},
              "thresholds": {
                "mode": "absolute",
                "steps": []
              },
              "unit": "short"
            },
            "overrides": []
          },
          "fill": 1,
          "fillGradient": 0,
          "gridPos": {
            "h": 9,
            "w": 12,
            "x": 0,
            "y": 19
          },
          "hiddenSeries": false,
          "id": 395,
          "legend": {
            "alignAsTable": true,
            "avg": false,
            "current": true,
            "max": false,
            "min": false,
            "show": true,
            "total": false,
            "values": true
          },
          "lines": true,
          "linewidth": 1,
          "nullPointMode": "connected",
          "options": {
            "alertThreshold": true
          },
          "percentage": false,
          "pluginVersion": "7.4.3",
          "pointradius": 2,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [],
          "spaceLength": 10,
          "stack": false,
          "steppedLine": false,
          "targets": [
            {
              "alias": "Disponible : $tag_host",
              "groupBy": [
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                }
              ],
              "measurement": "swap",
              "orderByTime": "ASC",
              "policy": "default",
              "refId": "A",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "free"
                    ],
                    "type": "field"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "projet",
                  "operator": "=~",
                  "value": "/^$project$/"
                }
              ]
            },
            {
              "alias": "Utilisé : $tag_host",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "hide": true,
              "measurement": "swap",
              "orderByTime": "ASC",
              "policy": "default",
              "refId": "B",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "used"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "projet",
                  "operator": "=~",
                  "value": "/^$project$/"
                }
              ]
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeRegions": [],
          "timeShift": null,
          "title": "SWAP",
          "tooltip": {
            "shared": true,
            "sort": 0,
            "value_type": "individual"
          },
          "type": "graph",
          "xaxis": {
            "buckets": null,
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "$$hashKey": "object:5971",
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            },
            {
              "$$hashKey": "object:5972",
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ],
          "yaxis": {
            "align": false,
            "alignLevel": null
          }
        },
        {
          "aliasColors": {},
          "bars": false,
          "dashLength": 10,
          "dashes": false,
          "datasource": null,
          "fieldConfig": {
            "defaults": {
              "color": {},
              "custom": {},
              "thresholds": {
                "mode": "absolute",
                "steps": []
              },
              "unit": "decbits"
            },
            "overrides": []
          },
          "fill": 1,
          "fillGradient": 0,
          "gridPos": {
            "h": 9,
            "w": 12,
            "x": 12,
            "y": 19
          },
          "hiddenSeries": false,
          "id": 262,
          "legend": {
            "alignAsTable": true,
            "avg": false,
            "current": true,
            "hideEmpty": false,
            "hideZero": false,
            "max": false,
            "min": false,
            "rightSide": false,
            "show": true,
            "total": false,
            "values": true
          },
          "lines": true,
          "linewidth": 1,
          "nullPointMode": "connected",
          "options": {
            "alertThreshold": true
          },
          "percentage": false,
          "pluginVersion": "7.4.3",
          "pointradius": 2,
          "points": false,
          "renderer": "flot",
          "repeat": null,
          "repeatDirection": "v",
          "seriesOverrides": [],
          "spaceLength": 10,
          "stack": false,
          "steppedLine": false,
          "targets": [
            {
              "alias": "Utilisé $tag_host",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "hide": false,
              "measurement": "disk",
              "orderByTime": "ASC",
              "policy": "default",
              "query": "SELECT 100 - mean(\"usage_idle\") FROM \"cpu\" WHERE (\"host\" =~ /^$server$/ AND \"time\" > now() - 4w) AND $timeFilter GROUP BY time($__interval) fill(null)",
              "rawQuery": false,
              "refId": "1 month - Mémoire utilisée",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "used"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": ">",
                  "value": "now() - 4w"
                },
                {
                  "condition": "AND",
                  "key": "projet",
                  "operator": "=~",
                  "value": "/^$project$/"
                }
              ]
            },
            {
              "alias": "Total $tag_host",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "hide": false,
              "measurement": "disk",
              "orderByTime": "ASC",
              "policy": "default",
              "query": "SELECT 100 - mean(\"usage_idle\") FROM \"cpu\" WHERE (\"host\" =~ /^$server$/ AND \"time\" > now() - 4w) AND $timeFilter GROUP BY time($__interval) fill(null)",
              "rawQuery": false,
              "refId": "1 month - Mémoire totale",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "total"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": ">",
                  "value": "now() - 4w"
                },
                {
                  "condition": "AND",
                  "key": "projet",
                  "operator": "=~",
                  "value": "/^$project$/"
                }
              ]
            },
            {
              "alias": "Utilisé (1min) $tag_host",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "hide": true,
              "measurement": "disk",
              "orderByTime": "ASC",
              "policy": "RP3month",
              "query": "SELECT 100 - mean(\"mean_usage_idle\") FROM \"RP3month\".\"cpu\" WHERE (\"host\" =~ /^$server$/ AND \"time\" < now() - 4w AND \"time\" > now() - 12w) AND $timeFilter GROUP BY time($__interval) fill(null)",
              "rawQuery": false,
              "refId": "3 month - Mémoire utilisée",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "mean_used"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": "<",
                  "value": "now() - 4w"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": ">",
                  "value": "now() - 12w"
                }
              ]
            },
            {
              "alias": "Total (1min) $tag_host",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "hide": true,
              "measurement": "disk",
              "orderByTime": "ASC",
              "policy": "RP3month",
              "query": "SELECT 100 - mean(\"mean_usage_idle\") FROM \"RP3month\".\"cpu\" WHERE (\"host\" =~ /^$server$/ AND \"time\" < now() - 4w AND \"time\" > now() - 12w) AND $timeFilter GROUP BY time($__interval) fill(null)",
              "rawQuery": false,
              "refId": "3 month - Mémoire totale",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "mean_total"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": "<",
                  "value": "now() - 4w"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": ">",
                  "value": "now() - 12w"
                }
              ]
            },
            {
              "alias": "Utilisé (10min) $tag_host",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "hide": true,
              "measurement": "disk",
              "orderByTime": "ASC",
              "policy": "RP6month",
              "query": "SELECT 100 - mean(\"mean_mean_usage_idle\") FROM \"RP6month\".\"cpu\" WHERE (\"host\" =~ /^$server$/ AND \"time\" < now() - 24w) AND $timeFilter GROUP BY time($__interval) fill(null)",
              "rawQuery": false,
              "refId": "6 month - Mémoire utilisée",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "mean_mean_used"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": "<",
                  "value": "now() - 24w"
                }
              ]
            },
            {
              "alias": "Total (10min) $tag_host",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "hide": true,
              "measurement": "disk",
              "orderByTime": "ASC",
              "policy": "RP6month",
              "query": "SELECT 100 - mean(\"mean_mean_usage_idle\") FROM \"RP6month\".\"cpu\" WHERE (\"host\" =~ /^$server$/ AND \"time\" < now() - 24w) AND $timeFilter GROUP BY time($__interval) fill(null)",
              "rawQuery": false,
              "refId": "6 month - Mémoire totale",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "mean_mean_total"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": "<",
                  "value": "now() - 24w"
                }
              ]
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeRegions": [],
          "timeShift": null,
          "title": "Utilisation $server",
          "tooltip": {
            "shared": true,
            "sort": 0,
            "value_type": "individual"
          },
          "transformations": [],
          "type": "graph",
          "xaxis": {
            "buckets": null,
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "$$hashKey": "object:4979",
              "format": "decbits",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            },
            {
              "$$hashKey": "object:4980",
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ],
          "yaxis": {
            "align": false,
            "alignLevel": null
          }
        }
      ],
      "title": "Disques",
      "type": "row"
    },
    {
      "collapsed": true,
      "datasource": null,
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 11
      },
      "id": 37,
      "panels": [
        {
          "aliasColors": {},
          "bars": false,
          "dashLength": 10,
          "dashes": false,
          "datasource": null,
          "fieldConfig": {
            "defaults": {
              "color": {},
              "custom": {},
              "thresholds": {
                "mode": "absolute",
                "steps": []
              },
              "unit": "percent"
            },
            "overrides": []
          },
          "fill": 1,
          "fillGradient": 0,
          "gridPos": {
            "h": 9,
            "w": 12,
            "x": 0,
            "y": 12
          },
          "hiddenSeries": false,
          "id": 51,
          "legend": {
            "alignAsTable": true,
            "avg": true,
            "current": true,
            "max": false,
            "min": false,
            "show": true,
            "total": false,
            "values": true
          },
          "lines": true,
          "linewidth": 1,
          "nullPointMode": "connected",
          "options": {
            "alertThreshold": true
          },
          "percentage": false,
          "pluginVersion": "7.4.3",
          "pointradius": 2,
          "points": false,
          "renderer": "flot",
          "repeat": null,
          "repeatDirection": "v",
          "seriesOverrides": [],
          "spaceLength": 10,
          "stack": false,
          "steppedLine": false,
          "targets": [
            {
              "alias": "$tag_host",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "measurement": "cpu",
              "orderByTime": "ASC",
              "policy": "default",
              "query": "SELECT mean(usage_idle\") FROM \"cpu\" WHERE (\"host\" =~ /^$server$/ AND \"time\" > now() - 4w) AND $timeFilter GROUP BY time($__interval), \"host\" fill(null)",
              "rawQuery": false,
              "refId": "A",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "usage_idle"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  },
                  {
                    "params": [
                      "*-1 +100"
                    ],
                    "type": "math"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": ">",
                  "value": "now() - 4w"
                },
                {
                  "condition": "AND",
                  "key": "projet",
                  "operator": "=~",
                  "value": "/^$project$/"
                }
              ]
            },
            {
              "alias": "$tag_host",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "hide": true,
              "measurement": "cpu",
              "orderByTime": "ASC",
              "policy": "RP3month",
              "query": "SELECT 100 - mean(\"mean_usage_idle\") FROM \"RP3month\".\"cpu\" WHERE (\"host\" =~ /^$server$/ AND \"time\" < now() - 4w AND \"time\" > now() - 12w) AND $timeFilter GROUP BY time($__interval) fill(null)",
              "rawQuery": false,
              "refId": "B",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "mean_usage_idle"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  },
                  {
                    "params": [
                      "*-1+100"
                    ],
                    "type": "math"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": "<",
                  "value": "now() - 4w"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": ">",
                  "value": "now() - 12w"
                },
                {
                  "condition": "AND",
                  "key": "projet",
                  "operator": "=~",
                  "value": "/^$project$/"
                }
              ]
            },
            {
              "alias": "$tag_host",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "hide": true,
              "measurement": "cpu",
              "orderByTime": "ASC",
              "policy": "RP6month",
              "query": "SELECT 100 - mean(\"mean_mean_usage_idle\") FROM \"RP6month\".\"cpu\" WHERE (\"host\" =~ /^$server$/ AND \"time\" < now() - 24w) AND $timeFilter GROUP BY time($__interval) fill(null)",
              "rawQuery": false,
              "refId": "C",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "mean_mean_usage_idle"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  },
                  {
                    "params": [
                      "*-1+100"
                    ],
                    "type": "math"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": "<",
                  "value": "now() - 24w"
                },
                {
                  "condition": "AND",
                  "key": "projet",
                  "operator": "=~",
                  "value": "/^$project$/"
                }
              ]
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeRegions": [],
          "timeShift": null,
          "title": "Utilisation Global % $server",
          "tooltip": {
            "shared": true,
            "sort": 0,
            "value_type": "individual"
          },
          "transformations": [],
          "type": "graph",
          "xaxis": {
            "buckets": null,
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "$$hashKey": "object:4139",
              "format": "percent",
              "label": null,
              "logBase": 1,
              "max": "100",
              "min": "0",
              "show": true
            },
            {
              "$$hashKey": "object:4140",
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ],
          "yaxis": {
            "align": false,
            "alignLevel": null
          }
        },
        {
          "aliasColors": {},
          "bars": false,
          "dashLength": 10,
          "dashes": false,
          "datasource": "telegraf",
          "editable": true,
          "error": false,
          "fieldConfig": {
            "defaults": {
              "color": {},
              "custom": {},
              "thresholds": {
                "mode": "absolute",
                "steps": []
              },
              "unit": "percent"
            },
            "overrides": []
          },
          "fill": 1,
          "fillGradient": 0,
          "grid": {},
          "gridPos": {
            "h": 9,
            "w": 12,
            "x": 12,
            "y": 12
          },
          "hiddenSeries": false,
          "id": 323,
          "isNew": true,
          "legend": {
            "alignAsTable": true,
            "avg": false,
            "current": true,
            "max": false,
            "min": false,
            "rightSide": false,
            "show": true,
            "total": false,
            "values": true
          },
          "lines": true,
          "linewidth": 1,
          "links": [],
          "nullPointMode": "connected",
          "options": {
            "alertThreshold": true
          },
          "paceLength": 10,
          "percentage": false,
          "pluginVersion": "7.4.3",
          "pointradius": 5,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [],
          "spaceLength": 10,
          "stack": false,
          "steppedLine": false,
          "targets": [
            {
              "alias": "User $tag_host",
              "dsType": "influxdb",
              "groupBy": [
                {
                  "params": [
                    "$interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "measurement": "cpu",
              "orderByTime": "ASC",
              "policy": "default",
              "refId": "A",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "usage_user"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "projet",
                  "operator": "=~",
                  "value": "/^$project$/"
                }
              ]
            },
            {
              "alias": "System $tag_host",
              "dsType": "influxdb",
              "groupBy": [
                {
                  "params": [
                    "$interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "measurement": "cpu",
              "orderByTime": "ASC",
              "policy": "default",
              "refId": "B",
              "resultFormat": "time_series",
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
                    "type": "mean"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "projet",
                  "operator": "=~",
                  "value": "/^$project$/"
                }
              ]
            },
            {
              "alias": "IoWait $tag_host",
              "dsType": "influxdb",
              "groupBy": [
                {
                  "params": [
                    "$interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "measurement": "cpu",
              "orderByTime": "ASC",
              "policy": "default",
              "refId": "C",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "usage_iowait"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "projet",
                  "operator": "=~",
                  "value": "/^$project$/"
                }
              ]
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeRegions": [],
          "timeShift": null,
          "title": "Utilisation by user (%)",
          "tooltip": {
            "msResolution": true,
            "ordering": "alphabetical",
            "shared": true,
            "sort": 0,
            "value_type": "cumulative"
          },
          "type": "graph",
          "xaxis": {
            "buckets": null,
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "$$hashKey": "object:1861",
              "format": "percent",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            },
            {
              "$$hashKey": "object:1862",
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ],
          "yaxis": {
            "align": false,
            "alignLevel": null
          }
        }
      ],
      "title": "CPU",
      "type": "row"
    },
    {
      "collapsed": true,
      "datasource": null,
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 12
      },
      "id": 67,
      "panels": [
        {
          "aliasColors": {},
          "bars": false,
          "dashLength": 10,
          "dashes": false,
          "datasource": null,
          "fieldConfig": {
            "defaults": {
              "color": {},
              "custom": {},
              "thresholds": {
                "mode": "absolute",
                "steps": []
              },
              "unit": "decbits"
            },
            "overrides": []
          },
          "fill": 1,
          "fillGradient": 0,
          "gridPos": {
            "h": 9,
            "w": 24,
            "x": 0,
            "y": 13
          },
          "hiddenSeries": false,
          "id": 81,
          "legend": {
            "alignAsTable": true,
            "avg": false,
            "current": true,
            "max": false,
            "min": false,
            "show": true,
            "total": false,
            "values": true
          },
          "lines": true,
          "linewidth": 1,
          "nullPointMode": "connected",
          "options": {
            "alertThreshold": true
          },
          "percentage": false,
          "pluginVersion": "7.4.3",
          "pointradius": 2,
          "points": false,
          "renderer": "flot",
          "repeat": null,
          "repeatDirection": "v",
          "seriesOverrides": [],
          "spaceLength": 10,
          "stack": false,
          "steppedLine": false,
          "targets": [
            {
              "alias": "Utilisé $tag_host",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "measurement": "mem",
              "orderByTime": "ASC",
              "policy": "default",
              "query": "SELECT 100 - mean(\"usage_idle\") FROM \"cpu\" WHERE (\"host\" =~ /^$server$/ AND \"time\" > now() - 4w) AND $timeFilter GROUP BY time($__interval) fill(null)",
              "rawQuery": false,
              "refId": "1 month - Mémoire utilisée",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "used"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": ">",
                  "value": "now() - 4w"
                },
                {
                  "condition": "AND",
                  "key": "projet",
                  "operator": "=~",
                  "value": "/^$project$/"
                }
              ]
            },
            {
              "alias": "Total $tag_host",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "hide": false,
              "measurement": "mem",
              "orderByTime": "ASC",
              "policy": "default",
              "query": "SELECT 100 - mean(\"usage_idle\") FROM \"cpu\" WHERE (\"host\" =~ /^$server$/ AND \"time\" > now() - 4w) AND $timeFilter GROUP BY time($__interval) fill(null)",
              "rawQuery": false,
              "refId": "1 month - Mémoire totale",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "total"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": ">",
                  "value": "now() - 4w"
                },
                {
                  "condition": "AND",
                  "key": "projet",
                  "operator": "=~",
                  "value": "/^$project$/"
                }
              ]
            },
            {
              "alias": "Utilisé (1min) $tag_host",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "hide": true,
              "measurement": "mem",
              "orderByTime": "ASC",
              "policy": "RP3month",
              "query": "SELECT 100 - mean(\"mean_usage_idle\") FROM \"RP3month\".\"cpu\" WHERE (\"host\" =~ /^$server$/ AND \"time\" < now() - 4w AND \"time\" > now() - 12w) AND $timeFilter GROUP BY time($__interval) fill(null)",
              "rawQuery": false,
              "refId": "3 month - Mémoire utilisée",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "mean_used"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": "<",
                  "value": "now() - 4w"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": ">",
                  "value": "now() - 12w"
                },
                {
                  "condition": "AND",
                  "key": "projet",
                  "operator": "=~",
                  "value": "/^$project$/"
                }
              ]
            },
            {
              "alias": "Total (1min) $tag_host",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "hide": true,
              "measurement": "mem",
              "orderByTime": "ASC",
              "policy": "RP3month",
              "query": "SELECT 100 - mean(\"mean_usage_idle\") FROM \"RP3month\".\"cpu\" WHERE (\"host\" =~ /^$server$/ AND \"time\" < now() - 4w AND \"time\" > now() - 12w) AND $timeFilter GROUP BY time($__interval) fill(null)",
              "rawQuery": false,
              "refId": "3 month - Mémoire totale",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "mean_total"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": "<",
                  "value": "now() - 4w"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": ">",
                  "value": "now() - 12w"
                },
                {
                  "condition": "AND",
                  "key": "projet",
                  "operator": "=~",
                  "value": "/^$project$/"
                }
              ]
            },
            {
              "alias": "Utilisé (10min)  $tag_host",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "hide": true,
              "measurement": "mem",
              "orderByTime": "ASC",
              "policy": "RP6month",
              "query": "SELECT 100 - mean(\"mean_mean_usage_idle\") FROM \"RP6month\".\"cpu\" WHERE (\"host\" =~ /^$server$/ AND \"time\" < now() - 24w) AND $timeFilter GROUP BY time($__interval) fill(null)",
              "rawQuery": false,
              "refId": "6 month - Mémoire utilisée",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "mean_mean_used"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": "<",
                  "value": "now() - 24w"
                },
                {
                  "condition": "AND",
                  "key": "projet",
                  "operator": "=~",
                  "value": "/^$project$/"
                }
              ]
            },
            {
              "alias": "Total (10min) $tag_host",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "hide": true,
              "measurement": "mem",
              "orderByTime": "ASC",
              "policy": "RP6month",
              "query": "SELECT 100 - mean(\"mean_mean_usage_idle\") FROM \"RP6month\".\"cpu\" WHERE (\"host\" =~ /^$server$/ AND \"time\" < now() - 24w) AND $timeFilter GROUP BY time($__interval) fill(null)",
              "rawQuery": false,
              "refId": "6 month - Mémoire totale",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "mean_mean_total"
                    ],
                    "type": "field"
                  },
                  {
                    "params": [],
                    "type": "mean"
                  }
                ]
              ],
              "tags": [
                {
                  "key": "host",
                  "operator": "=~",
                  "value": "/^$server$/"
                },
                {
                  "condition": "AND",
                  "key": "time",
                  "operator": "<",
                  "value": "now() - 24w"
                },
                {
                  "condition": "AND",
                  "key": "projet",
                  "operator": "=~",
                  "value": "/^$project$/"
                }
              ]
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeRegions": [],
          "timeShift": null,
          "title": "Utilisation $server",
          "tooltip": {
            "shared": true,
            "sort": 0,
            "value_type": "individual"
          },
          "transformations": [],
          "type": "graph",
          "xaxis": {
            "buckets": null,
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "$$hashKey": "object:6491",
              "format": "decbits",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            },
            {
              "$$hashKey": "object:6492",
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ],
          "yaxis": {
            "align": false,
            "alignLevel": null
          }
        }
      ],
      "title": "Mémoire",
      "type": "row"
    },
    {
      "collapsed": true,
      "datasource": null,
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 13
      },
      "id": 411,
      "panels": [
        {
          "aliasColors": {},
          "bars": false,
          "dashLength": 10,
          "dashes": false,
          "datasource": null,
          "description": "",
          "fieldConfig": {
            "defaults": {
              "custom": {}
            },
            "overrides": []
          },
          "fill": 1,
          "fillGradient": 0,
          "gridPos": {
            "h": 10,
            "w": 24,
            "x": 0,
            "y": 14
          },
          "hiddenSeries": false,
          "id": 427,
          "legend": {
            "alignAsTable": true,
            "avg": false,
            "current": true,
            "max": false,
            "min": false,
            "show": true,
            "total": false,
            "values": true
          },
          "lines": true,
          "linewidth": 1,
          "nullPointMode": "connected",
          "options": {
            "alertThreshold": true
          },
          "percentage": false,
          "pluginVersion": "7.4.3",
          "pointradius": 2,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [],
          "spaceLength": 10,
          "stack": false,
          "steppedLine": false,
          "targets": [
            {
              "alias": "Established : $tag_host",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "measurement": "netstat",
              "orderByTime": "ASC",
              "policy": "default",
              "refId": "A",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "tcp_established"
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
                },
                {
                  "condition": "AND",
                  "key": "projet",
                  "operator": "=~",
                  "value": "/^$project$/"
                }
              ]
            },
            {
              "alias": "Close : $tag_host",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "hide": false,
              "measurement": "netstat",
              "orderByTime": "ASC",
              "policy": "default",
              "refId": "B",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "tcp_close"
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
                },
                {
                  "condition": "AND",
                  "key": "projet",
                  "operator": "=~",
                  "value": "/^$project$/"
                }
              ]
            },
            {
              "alias": "Listen : $tag_host",
              "groupBy": [
                {
                  "params": [
                    "$__interval"
                  ],
                  "type": "time"
                },
                {
                  "params": [
                    "host"
                  ],
                  "type": "tag"
                },
                {
                  "params": [
                    "null"
                  ],
                  "type": "fill"
                }
              ],
              "hide": false,
              "measurement": "netstat",
              "orderByTime": "ASC",
              "policy": "default",
              "refId": "C",
              "resultFormat": "time_series",
              "select": [
                [
                  {
                    "params": [
                      "tcp_listen"
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
                },
                {
                  "condition": "AND",
                  "key": "projet",
                  "operator": "=~",
                  "value": "/^$project$/"
                }
              ]
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeRegions": [],
          "timeShift": null,
          "title": "TCP Connexion $server",
          "tooltip": {
            "shared": true,
            "sort": 0,
            "value_type": "individual"
          },
          "type": "graph",
          "xaxis": {
            "buckets": null,
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            },
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ],
          "yaxis": {
            "align": false,
            "alignLevel": null
          }
        }
      ],
      "title": "Réseaux",
      "type": "row"
    }
  ],
  "refresh": "10s",
  "schemaVersion": 27,
  "style": "dark",
  "tags": [
    "ydays",
    "ynov",
    "global",
    "monitoring"
  ],
  "templating": {
    "list": [
      {
        "allValue": null,
        "current": {
          "selected": true,
          "text": "devops-monitoring",
          "value": "devops-monitoring"
        },
        "datasource": null,
        "definition": "SHOW TAG VALUES WITH key = \"projet\"",
        "description": null,
        "error": null,
        "hide": 0,
        "includeAll": false,
        "label": "Project",
        "multi": false,
        "name": "project",
        "options": [
          {
            "selected": false,
            "text": "devops-cloudvm",
            "value": "devops-cloudvm"
          },
          {
            "selected": true,
            "text": "devops-monitoring",
            "value": "devops-monitoring"
          }
        ],
        "query": "SHOW TAG VALUES WITH key = \"projet\"",
        "refresh": 0,
        "regex": "",
        "skipUrlSync": false,
        "sort": 0,
        "tagValuesQuery": "",
        "tags": [],
        "tagsQuery": "",
        "type": "query",
        "useTags": false
      },
      {
        "allValue": ".*",
        "current": {
          "selected": true,
          "text": [
            "All"
          ],
          "value": [
            "$__all"
          ]
        },
        "datasource": null,
        "definition": "SHOW TAG VALUES WITH key = \"host\" WHERE \"projet\" =~ /^$project$/",
        "description": null,
        "error": null,
        "hide": 0,
        "includeAll": true,
        "label": "Server",
        "multi": true,
        "name": "server",
        "options": [],
        "query": "SHOW TAG VALUES WITH key = \"host\" WHERE \"projet\" =~ /^$project$/",
        "refresh": 2,
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
  "timepicker": {
    "refresh_intervals": [
      "5s",
      "10s",
      "30s",
      "1m",
      "5m",
      "15m",
      "30m",
      "1h",
      "2h",
      "1d"
    ]
  },
  "timezone": "",
  "title": "Dashboard Global",
  "uid": "qsdsqzddqzdqsi",
  "version": 14
}
```
