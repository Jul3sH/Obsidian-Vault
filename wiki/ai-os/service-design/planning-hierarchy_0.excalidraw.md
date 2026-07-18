---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠== You can decompress Drawing data with the command palette: 'Decompress current Excalidraw file'. For more info check in plugin settings under 'Saving'

# Excalidraw Data

## Text Elements
Planning Hierarchy ^title1

Goals -> Projects -> Deliverables -> Timebox ^sub1

Goals
6 workstreams, quarterly
(SMART + OKR) ^goals_t

Projects
Objective + Outcomes/Outputs + WSJF
/project-planner ^proj_t

Gate: worth starting? ^gate1

Deliverables
user-facing, enablers, generic
/define-user-story + /define-enabler ^deliv_t

Gate: scoped + sized + value-linked? ^gate2

Timebox (1 week)
MoSCoW committed & tracked
/timebox-plan + /jira-sync ^IBQe1p99

Ceremonies & Prioritisation ^f8ZnlVcG

Daily stand-up
6:00 AM HKT, Mon-Fri (~5 min) ^cer1_t

Timebox planning
Weekend (~45 min), /timebox-plan ^cer2_t

Retrospective
Friday 4:00 PM HKT (~20 min), /retro ^cer3_t

Prioritisation
Projects: WSJF (rank initiatives)
Timebox: MoSCoW 60/20/20 ^prio_t

Guardrails
Must Haves <= 60% of capacity
WIP limit: 2 Implementing Projects ^guard_t

Project flow stages (funnel/review/ready/implementing/done) -> see Portfolio Kanban diagram ^footer1

## Drawing
```json
{
	"type": "excalidraw",
	"version": 2,
	"source": "https://excalidraw.com",
	"elements": [
		{
			"type": "text",
			"x": 261,
			"y": 10,
			"width": 216,
			"height": 30,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 911638886,
			"version": 1,
			"versionNonce": 1194200939,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "title1",
			"fontSize": 24,
			"fontFamily": 1,
			"text": "Planning Hierarchy",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Planning Hierarchy",
			"lineHeight": 1.25,
			"baseline": 30
		},
		{
			"type": "text",
			"x": 193,
			"y": 42,
			"width": 308,
			"height": 17.5,
			"angle": 0,
			"strokeColor": "#757575",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 89256606,
			"version": 1,
			"versionNonce": 1456784982,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "sub1",
			"fontSize": 14,
			"fontFamily": 1,
			"text": "Goals -> Projects -> Deliverables -> Timebox",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Goals -> Projects -> Deliverables -> Timebox",
			"lineHeight": 1.25,
			"baseline": 17.5
		},
		{
			"type": "rectangle",
			"x": 50,
			"y": 70,
			"width": 320,
			"height": 80,
			"angle": 0,
			"strokeColor": "#1c64c7",
			"backgroundColor": "#a5d8ff",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 520579924,
			"version": 1,
			"versionNonce": 2088872236,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "goals_t"
				},
				{
					"type": "arrow",
					"id": "hA1"
				}
			],
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "goals"
		},
		{
			"type": "text",
			"x": 114,
			"y": 80,
			"width": 192,
			"height": 60,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 258405698,
			"version": 1,
			"versionNonce": 164430431,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "goals_t",
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Goals\n6 workstreams, quarterly\n(SMART + OKR)",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "goals",
			"originalText": "Goals\n6 workstreams, quarterly\n(SMART + OKR)",
			"lineHeight": 1.25,
			"baseline": 60
		},
		{
			"type": "rectangle",
			"x": 50,
			"y": 188,
			"width": 320,
			"height": 80,
			"angle": 0,
			"strokeColor": "#6d28d9",
			"backgroundColor": "#d0bfff",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 1547267971,
			"version": 1,
			"versionNonce": 1306934251,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "proj_t"
				},
				{
					"type": "arrow",
					"id": "hA1"
				},
				{
					"type": "arrow",
					"id": "hA2"
				}
			],
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "proj"
		},
		{
			"type": "text",
			"x": 70,
			"y": 198,
			"width": 280,
			"height": 60,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1326351832,
			"version": 1,
			"versionNonce": 1729109808,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "proj_t",
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Projects\nObjective + Outcomes/Outputs + WSJF\n/project-planner",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "proj",
			"originalText": "Projects\nObjective + Outcomes/Outputs + WSJF\n/project-planner",
			"lineHeight": 1.25,
			"baseline": 60
		},
		{
			"type": "arrow",
			"x": 210,
			"y": 150,
			"width": 0,
			"height": 38,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 642459453,
			"version": 1,
			"versionNonce": 1500446299,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "hA1",
			"points": [
				[
					0,
					0
				],
				[
					0,
					38
				]
			],
			"lastCommittedPoint": null,
			"startBinding": {
				"elementId": "goals",
				"focus": 0,
				"gap": 4,
				"fixedPoint": [
					0.5,
					1
				]
			},
			"endBinding": {
				"elementId": "proj",
				"focus": 0,
				"gap": 4,
				"fixedPoint": [
					0.5,
					0
				]
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"type": "text",
			"x": 137,
			"y": 272,
			"width": 147,
			"height": 17.5,
			"angle": 0,
			"strokeColor": "#757575",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 4618508,
			"version": 1,
			"versionNonce": 475079242,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "gate1",
			"fontSize": 14,
			"fontFamily": 1,
			"text": "Gate: worth starting?",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Gate: worth starting?",
			"lineHeight": 1.25,
			"baseline": 17.5
		},
		{
			"type": "rectangle",
			"x": 50,
			"y": 330,
			"width": 320,
			"height": 80,
			"angle": 0,
			"strokeColor": "#b45309",
			"backgroundColor": "#fff3bf",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 1035428321,
			"version": 1,
			"versionNonce": 639259246,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "deliv_t"
				},
				{
					"type": "arrow",
					"id": "hA2"
				},
				{
					"type": "arrow",
					"id": "hA3"
				}
			],
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "deliv"
		},
		{
			"type": "text",
			"x": 66,
			"y": 340,
			"width": 288,
			"height": 60,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 176513076,
			"version": 1,
			"versionNonce": 800154062,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "deliv_t",
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Deliverables\nuser-facing, enablers, generic\n/define-user-story + /define-enabler",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "deliv",
			"originalText": "Deliverables\nuser-facing, enablers, generic\n/define-user-story + /define-enabler",
			"lineHeight": 1.25,
			"baseline": 60
		},
		{
			"type": "arrow",
			"x": 210,
			"y": 296,
			"width": 0,
			"height": 34,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1475212395,
			"version": 1,
			"versionNonce": 1374586503,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "hA2",
			"points": [
				[
					0,
					0
				],
				[
					0,
					34
				]
			],
			"lastCommittedPoint": null,
			"startBinding": {
				"elementId": "proj",
				"focus": 0,
				"gap": 4,
				"fixedPoint": [
					0.5,
					1
				]
			},
			"endBinding": {
				"elementId": "deliv",
				"focus": 0,
				"gap": 4,
				"fixedPoint": [
					0.5,
					0
				]
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"type": "text",
			"x": 80,
			"y": 414,
			"width": 252,
			"height": 17.5,
			"angle": 0,
			"strokeColor": "#757575",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1692747984,
			"version": 1,
			"versionNonce": 649324830,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "gate2",
			"fontSize": 14,
			"fontFamily": 1,
			"text": "Gate: scoped + sized + value-linked?",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Gate: scoped + sized + value-linked?",
			"lineHeight": 1.25,
			"baseline": 17.5
		},
		{
			"type": "rectangle",
			"x": 50,
			"y": 470,
			"width": 320,
			"height": 80,
			"angle": 0,
			"strokeColor": "#15803d",
			"backgroundColor": "#b2f2bb",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 1897098009,
			"version": 1,
			"versionNonce": 1463538902,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "IBQe1p99"
				},
				{
					"type": "arrow",
					"id": "hA3"
				}
			],
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "timebox"
		},
		{
			"type": "text",
			"x": 106,
			"y": 480,
			"width": 208,
			"height": 60,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 502540548,
			"version": 1,
			"versionNonce": 2116931302,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "IBQe1p99",
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Timebox (1 week)\nMoSCoW committed & tracked\n/timebox-plan + /jira-sync",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "timebox",
			"originalText": "Timebox (1 week)\nMoSCoW committed & tracked\n/timebox-plan + /jira-sync",
			"lineHeight": 1.25,
			"baseline": 60
		},
		{
			"type": "arrow",
			"x": 210,
			"y": 438,
			"width": 0,
			"height": 32,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 2019364243,
			"version": 1,
			"versionNonce": 656739632,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "hA3",
			"points": [
				[
					0,
					0
				],
				[
					0,
					32
				]
			],
			"lastCommittedPoint": null,
			"startBinding": {
				"elementId": "deliv",
				"focus": 0,
				"gap": 4,
				"fixedPoint": [
					0.5,
					1
				]
			},
			"endBinding": {
				"elementId": "timebox",
				"focus": 0,
				"gap": 4,
				"fixedPoint": [
					0.5,
					0
				]
			},
			"startArrowhead": null,
			"endArrowhead": "arrow"
		},
		{
			"type": "rectangle",
			"x": 410,
			"y": 60,
			"width": 350,
			"height": 510,
			"angle": 0,
			"strokeColor": "#8b5cf6",
			"backgroundColor": "#e5dbff",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 30,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 2063582861,
			"version": 1,
			"versionNonce": 1697907494,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "zone"
		},
		{
			"type": "text",
			"x": 430,
			"y": 68,
			"width": 243,
			"height": 22.5,
			"angle": 0,
			"strokeColor": "#5b21b6",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 656779043,
			"version": 1,
			"versionNonce": 223316926,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "f8ZnlVcG",
			"fontSize": 18,
			"fontFamily": 1,
			"text": "Ceremonies & Prioritisation",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Ceremonies & Prioritisation",
			"lineHeight": 1.25,
			"baseline": 22.5
		},
		{
			"type": "rectangle",
			"x": 430,
			"y": 105,
			"width": 310,
			"height": 75,
			"angle": 0,
			"strokeColor": "#b45309",
			"backgroundColor": "#fff3bf",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 1591112060,
			"version": 1,
			"versionNonce": 1214026199,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "cer1_t"
				}
			],
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "cer1"
		},
		{
			"type": "text",
			"x": 469,
			"y": 122.5,
			"width": 232,
			"height": 40,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 2054350652,
			"version": 1,
			"versionNonce": 1237432422,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "cer1_t",
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Daily stand-up\n6:00 AM HKT, Mon-Fri (~5 min)",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "cer1",
			"originalText": "Daily stand-up\n6:00 AM HKT, Mon-Fri (~5 min)",
			"lineHeight": 1.25,
			"baseline": 40
		},
		{
			"type": "rectangle",
			"x": 430,
			"y": 195,
			"width": 310,
			"height": 75,
			"angle": 0,
			"strokeColor": "#b45309",
			"backgroundColor": "#fff3bf",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 94352121,
			"version": 1,
			"versionNonce": 918582546,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "cer2_t"
				}
			],
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "cer2"
		},
		{
			"type": "text",
			"x": 457,
			"y": 212.5,
			"width": 256,
			"height": 40,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 987234004,
			"version": 1,
			"versionNonce": 675586059,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "cer2_t",
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Timebox planning\nWeekend (~45 min), /timebox-plan",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "cer2",
			"originalText": "Timebox planning\nWeekend (~45 min), /timebox-plan",
			"lineHeight": 1.25,
			"baseline": 40
		},
		{
			"type": "rectangle",
			"x": 430,
			"y": 285,
			"width": 310,
			"height": 75,
			"angle": 0,
			"strokeColor": "#b45309",
			"backgroundColor": "#fff3bf",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 718111936,
			"version": 1,
			"versionNonce": 1872473018,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "cer3_t"
				}
			],
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "cer3"
		},
		{
			"type": "text",
			"x": 441,
			"y": 302.5,
			"width": 288,
			"height": 40,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 808162956,
			"version": 1,
			"versionNonce": 1134367765,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "cer3_t",
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Retrospective\nFriday 4:00 PM HKT (~20 min), /retro",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "cer3",
			"originalText": "Retrospective\nFriday 4:00 PM HKT (~20 min), /retro",
			"lineHeight": 1.25,
			"baseline": 40
		},
		{
			"type": "rectangle",
			"x": 430,
			"y": 375,
			"width": 310,
			"height": 90,
			"angle": 0,
			"strokeColor": "#0f766e",
			"backgroundColor": "#c3fae8",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 1129108664,
			"version": 1,
			"versionNonce": 1734309120,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "prio_t"
				}
			],
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "prio"
		},
		{
			"type": "text",
			"x": 453,
			"y": 390,
			"width": 264,
			"height": 60,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 310201480,
			"version": 1,
			"versionNonce": 1420345781,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "prio_t",
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Prioritisation\nProjects: WSJF (rank initiatives)\nTimebox: MoSCoW 60/20/20",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "prio",
			"originalText": "Prioritisation\nProjects: WSJF (rank initiatives)\nTimebox: MoSCoW 60/20/20",
			"lineHeight": 1.25,
			"baseline": 60
		},
		{
			"type": "rectangle",
			"x": 430,
			"y": 480,
			"width": 310,
			"height": 80,
			"angle": 0,
			"strokeColor": "#b45309",
			"backgroundColor": "#ffd8a8",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"seed": 1380709100,
			"version": 1,
			"versionNonce": 1360977933,
			"isDeleted": false,
			"boundElements": [
				{
					"type": "text",
					"id": "guard_t"
				}
			],
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "guard"
		},
		{
			"type": "text",
			"x": 449,
			"y": 490,
			"width": 272,
			"height": 60,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1238015052,
			"version": 1,
			"versionNonce": 532635122,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "guard_t",
			"fontSize": 16,
			"fontFamily": 1,
			"text": "Guardrails\nMust Haves <= 60% of capacity\nWIP limit: 2 Implementing Projects",
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "guard",
			"originalText": "Guardrails\nMust Haves <= 60% of capacity\nWIP limit: 2 Implementing Projects",
			"lineHeight": 1.25,
			"baseline": 60
		},
		{
			"type": "text",
			"x": 60,
			"y": 565,
			"width": 637,
			"height": 17.5,
			"angle": 0,
			"strokeColor": "#757575",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 2041751271,
			"version": 1,
			"versionNonce": 1343787667,
			"isDeleted": false,
			"boundElements": null,
			"updated": 1781394168744,
			"link": null,
			"locked": false,
			"id": "footer1",
			"fontSize": 14,
			"fontFamily": 1,
			"text": "Project flow stages (funnel/review/ready/implementing/done) -> see Portfolio Kanban diagram",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Project flow stages (funnel/review/ready/implementing/done) -> see Portfolio Kanban diagram",
			"lineHeight": 1.25,
			"baseline": 17.5
		}
	],
	"appState": {
		"gridSize": null,
		"viewBackgroundColor": "#ffffff"
	},
	"files": {}
}
```
%%