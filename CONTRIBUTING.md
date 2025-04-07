# Contributing Guide

## Clone & Branch

git clone git@github.com:Epec-Engineering/<repo>.git
git checkout -b feat/<ticket-id>-description

## Commit Style

Use Conventional Commits (https://www.conventionalcommits.org/):

type(scope): short message
e.g. feat(ci): add markdown‑lint workflow

## Pre‑commit Hooks

# Install tooling once

pip install pre-commit

# Activate hooks in this repo

pre-commit install
