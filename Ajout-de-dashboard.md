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
  "id": 1,
  "iteration": 1615054058649,
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
        "h": 4,
        "w": 10,
        "x": 0,
        "y": 0
      },
      "id": 146,
      "options": {
        "content": "<h3 style=\"text-align:center; margin-top: 5%; font-size:4em\">${project}</h3>",
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
        "h": 4,
        "w": 9,
        "x": 10,
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
        "y": 4
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
        "h": 3,
        "w": 3,
        "x": 0,
        "y": 5
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
          "selected": true,
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
        "h": 3,
        "w": 2,
        "x": 3,
        "y": 5
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
          "selected": true,
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
        "h": 3,
        "w": 3,
        "x": 5,
        "y": 5
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
          "selected": true,
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
          "query": "SELECT 100  - last(\"usage_idle\") FROM \"cpu\" WHERE (\"host\" =~ /^$server$/) AND $timeFilter GROUP BY time($interval)",
          "rawQuery": true,
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
                  "-100"
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
        "h": 3,
        "w": 3,
        "x": 8,
        "y": 5
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
          "selected": true,
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
        "h": 3,
        "w": 3,
        "x": 11,
        "y": 5
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
          "selected": true,
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
            }
          ]
        }
      ],
      "timeFrom": null,
      "timeShift": null,
      "title": "Disk Use",
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
        "h": 3,
        "w": 3,
        "x": 14,
        "y": 5
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
          "selected": true,
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
        "h": 3,
        "w": 2,
        "x": 17,
        "y": 5
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
          "selected": true,
          "text": "devops-ansible",
          "value": "devops-ansible"
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
          "groupBy": [
            {
              "params": [
                "$interval"
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
      "collapsed": false,
      "datasource": null,
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 8
      },
      "id": 37,
      "panels": [],
      "title": "CPU",
      "type": "row"
    },
    {
      "datasource": null,
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "palette-classic"
          },
          "custom": {
            "axisLabel": "",
            "axisPlacement": "auto",
            "barAlignment": 0,
            "drawStyle": "line",
            "fillOpacity": 10,
            "gradientMode": "none",
            "hideFrom": {
              "graph": false,
              "legend": false,
              "tooltip": false
            },
            "lineInterpolation": "linear",
            "lineWidth": 1,
            "pointSize": 5,
            "scaleDistribution": {
              "type": "linear"
            },
            "showPoints": "never",
            "spanNulls": true
          },
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "short"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 7,
        "w": 9,
        "x": 0,
        "y": 9
      },
      "id": 51,
      "options": {
        "graph": {},
        "legend": {
          "calcs": [],
          "displayMode": "list",
          "placement": "bottom"
        },
        "tooltipOptions": {
          "mode": "single"
        }
      },
      "pluginVersion": "7.4.3",
      "repeat": "server",
      "repeatDirection": "v",
      "scopedVars": {
        "server": {
          "selected": true,
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
          "measurement": "cpu",
          "orderByTime": "ASC",
          "policy": "default",
          "query": "SELECT 100 - mean(\"usage_idle\") FROM \"cpu\" WHERE (\"host\" =~ /^$server$/ AND \"time\" > now() - 4w) AND $timeFilter GROUP BY time($__interval) fill(null)",
          "rawQuery": true,
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
          "hide": false,
          "measurement": "cpu",
          "orderByTime": "ASC",
          "policy": "RP3month",
          "query": "SELECT 100 - mean(\"mean_usage_idle\") FROM \"RP3month\".\"cpu\" WHERE (\"host\" =~ /^$server$/ AND \"time\" < now() - 4w AND \"time\" > now() - 12w) AND $timeFilter GROUP BY time($__interval) fill(null)",
          "rawQuery": true,
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
          "hide": false,
          "measurement": "cpu",
          "orderByTime": "ASC",
          "policy": "RP6month",
          "query": "SELECT 100 - mean(\"mean_mean_usage_idle\") FROM \"RP6month\".\"cpu\" WHERE (\"host\" =~ /^$server$/ AND \"time\" < now() - 24w) AND $timeFilter GROUP BY time($__interval) fill(null)",
          "rawQuery": true,
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
      "title": "CPU Usage $server",
      "transformations": [],
      "type": "timeseries"
    },
    {
      "collapsed": false,
      "datasource": null,
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 16
      },
      "id": 67,
      "panels": [],
      "title": "Mémoire",
      "type": "row"
    },
    {
      "datasource": null,
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "palette-classic"
          },
          "custom": {
            "axisLabel": "",
            "axisPlacement": "auto",
            "barAlignment": 0,
            "drawStyle": "line",
            "fillOpacity": 10,
            "gradientMode": "none",
            "hideFrom": {
              "graph": false,
              "legend": false,
              "tooltip": false
            },
            "lineInterpolation": "linear",
            "lineWidth": 1,
            "pointSize": 5,
            "scaleDistribution": {
              "type": "linear"
            },
            "showPoints": "never",
            "spanNulls": true
          },
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
          "unit": "decbits"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 7,
        "w": 9,
        "x": 0,
        "y": 17
      },
      "id": 81,
      "options": {
        "graph": {},
        "legend": {
          "calcs": [],
          "displayMode": "list",
          "placement": "bottom"
        },
        "tooltipOptions": {
          "mode": "single"
        }
      },
      "pluginVersion": "7.4.3",
      "repeat": "server",
      "repeatDirection": "v",
      "scopedVars": {
        "server": {
          "selected": true,
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
            }
          ]
        },
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
            }
          ]
        },
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
          "hide": false,
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
            }
          ]
        },
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
          "hide": false,
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
            }
          ]
        },
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
          "hide": false,
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
            }
          ]
        },
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
          "hide": false,
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
            }
          ]
        }
      ],
      "title": "Mémoire Usage $server",
      "transformations": [],
      "type": "timeseries"
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
                "value": 700000000
              },
              {
                "color": "red",
                "value": 800000000
              }
            ]
          },
          "unit": "decbytes"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 7,
        "w": 4,
        "x": 9,
        "y": 17
      },
      "id": 99,
      "options": {
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "",
          "values": false
        },
        "showThresholdLabels": false,
        "showThresholdMarkers": true,
        "text": {}
      },
      "pluginVersion": "7.4.3",
      "repeat": "server",
      "repeatDirection": "v",
      "scopedVars": {
        "server": {
          "selected": true,
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
          "measurement": "mem",
          "orderByTime": "ASC",
          "policy": "default",
          "refId": "A",
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
      "title": "Mémoire utilisée $server",
      "type": "gauge"
    },
    {
      "datasource": null,
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "custom": {},
          "decimals": 0,
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
          "unit": "decbytes"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 7,
        "w": 2,
        "x": 13,
        "y": 17
      },
      "id": 101,
      "options": {
        "colorMode": "value",
        "graphMode": "none",
        "justifyMode": "auto",
        "orientation": "auto",
        "reduceOptions": {
          "calcs": [
            "lastNotNull"
          ],
          "fields": "",
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
          "selected": true,
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
          "measurement": "mem",
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
      "title": "Mémoire totale $server",
      "type": "stat"
    }
  ],
  "refresh": "10s",
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
          "selected": true,
          "text": [
            "devops-ansible"
          ],
          "value": [
            "devops-ansible"
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
  "version": 34
}
```