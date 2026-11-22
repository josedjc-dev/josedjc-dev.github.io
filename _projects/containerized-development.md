---
title: "Migrating Local Development to Docker Compose"
summary: "A repeatable Flask and SQLite development environment with live code reload, a browser-based database viewer, and a separate training lab."
status: "Implemented"
order: 1
skills:
  - Docker Compose
  - Flask
  - SQLite
  - Integration Testing
  - Technical Documentation
---

## The problem

The original Flask setup worked on my Mac. Getting started meant creating a Python environment, initializing SQLite, and starting Flask and Datasette in separate terminals. I wanted a setup that another developer or learner could reproduce and clean up with a few commands.

## What changed

Docker Compose now starts both services. Flask initializes and queries a SQLite database in a Docker volume. Datasette mounts the same volume read-only so a learner can inspect the data in a browser. Both ports are bound to the developer’s machine.

For development, a Compose override mounts the local Python source and enables Flask’s reloader. The training lab builds from the supplied source files and uses its own database volume. The original Python setup remains available for readers who want to follow each startup step.

## What I verified

- Flask and Datasette returned the same sample project from SQLite.
- Sending POST to the read-only Flask route returned HTTP 405.
- Editing Python in a test checkout reloaded Flask without rebuilding the image.
- Teardown removed the lab containers, network, database volume, and locally built images.

The checks ran on an Apple Silicon Mac using Docker Engine through Colima. This project moved the **local development setup** to containers. The public portfolio still runs on GitHub Pages.

## Try the review exercise

Imagine Flask returns a project name that differs from what you see in the database viewer. Where would you check first? Start by comparing the record’s slug and confirming that both services are reading the same SQLite volume. Then check which columns Flask selects and how the route turns the row into JSON.

## How I worked

I set the project goals, chose the direction for the visitor lab, and worked through the Flask, SQLite, and GitHub Actions exercises. OpenAI Codex assisted with the container setup, automated checks, documentation, and training material.
