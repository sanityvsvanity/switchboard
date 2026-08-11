# Switchboard

An AI agent that runs the phones for inbound sales teams. It answers every inbound call, qualifies callers through structured questions, books appointments into real calendar slots and logs a structured summary of every conversation with the transcript and recording attached.

## Problem

A Melbourne client was missing inbound sales calls after hours and during peak periods. Every missed call was a lost lead, and staffing the phones around the clock was not viable.

## Build

- Telephony: Twilio SIP trunking routes calls to the agent
- Voice runtime: Retell handles speech to text, text to speech and real time inference
- LLM: GPT-5 mini for low latency voice turns
- Automation: N8N workflows log structured call summaries and book appointments through Calendly
- Logs: full transcript and recording stored for every call

## The prompt does the heavy lifting

[prompts/system-prompt.txt](prompts/system-prompt.txt) is the production system prompt, templated for reuse. If you are building voice agents it is the most useful file in this repo:

- Slot capture, one question at a time, into a strict JSON schema: budget band, requirements, add-ons, timeframe, funding status, buyer type, preferred locations
- Pronunciation rules for prices and phone numbers in Australian English
- Small talk handled with a two turn budget, then a polite steer back to qualification
- Barge-in allowed, four second silence recovery, out of scope requests get a referral instead of an improvised answer
- STOP and opt-out requests logged as compliance flags
- Every call ends with a function call that logs the structured summary before hangup, never read aloud

## Result

The agent handles the full flow: greets, qualifies across nine slots, recommends options against budget bands with an "indicative only" disclaimer, offers real appointment slots, confirms bookings with an ID, and the sales team walks into every conversation pre-briefed.

## Repo layout

- `prompts/system-prompt.txt`: templated production system prompt
- `config/n8n-workflow.json`: logging and booking workflow, a simplified export for reference rather than the production graph

## Who built this

Gagan Dasari. I run [GTMpro](https://gtmpro.com.au), an agentic GTM engineering practice in Melbourne. Switchboard is one of the systems in the [catalogue](https://gtmpro.com.au).

gagan@gtmpro.com.au · [LinkedIn](https://www.linkedin.com/in/gaganbuilds) · [GitHub](https://github.com/sanityvsvanity)
