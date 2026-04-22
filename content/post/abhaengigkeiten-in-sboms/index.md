---
title: "Abhängigkeiten in SBOMs"
date: 2026-04-22T12:08:48+02:00
tags: 
  - SBOM
  - Cybersecurity
description: "Man sollte sich nicht auf die Passage im Cyber Resilience Act verlassen, wonach nur Abhängigkeiten auf oberster Ebene in SBOMs aufgenommen werden müssen."
image: ""
aliases: []
draft: false
---
Der CRA verlangt zwar nur „top-level dependencies“ in SBOMs, aber das ist „at the very least“ und beißt sich etwas mit den Due-Diligence-Anforderungen, die auch im CRA stehen. Außerdem erzählte mir ein EU-Lobbyist der Eclipse Foundation kürzlich, sowohl mit dem Digital Omnibus als auch im CRA-Review (noch vor 2030 geplant!) könne diese Anforderung noch ausgeweitet werden.

Und der entsprechende [Technical Report des BSI](https://www.bsi.bund.de/SharedDocs/Downloads/EN/BSI/Publications/TechGuidelines/TR03183/BSI-TR-03183-2_v2_1_0.pdf?__blob=publicationFile&v=5) sagt sogar folgendes:

> For an SBOM that is compliant with this Technical Guideline, recursive dependency resolution MUST be performed at least for each component included in the scope of delivery on each path downward (see Appendix, section 8.1.12) at least up to and including the first component that is outside the scope of delivery (see Appendix, section 8.1.11; for „delivery item SBOM“, see Appendix, section 8.3.4).

Das BSI ist besonders relevant, weil es die zuständige Marktüberwachungsbehörde in Deutschland ist, und außerdem scheinen auch Unternehmen anderer Länder (ich hörte Beispiele sowohl aus Amerika als auch aus China) diesen Report als Grundlage für die SBOM-Einführung zu nehmen, weil sonst wenige Handreichungen existieren.