# Upstream skill attribution

The three skills in this directory — `neo4j-cli-tools-skill`, `neo4j-cypher-skill`,
and `neo4j-migration-skill` — are vendored from
[neo4j-contrib/neo4j-skills](https://github.com/neo4j-contrib/neo4j-skills) at
commit `8e15b4b6975161744f373cd73704367dfded7115` and distributed under the
MIT License reproduced below.

To update, re-clone upstream and overwrite the three skill directories:

```sh
git clone --depth 1 https://github.com/neo4j-contrib/neo4j-skills.git /tmp/neo4j-skills
cp -R /tmp/neo4j-skills/neo4j-{cli-tools,cypher,migration}-skill plugins/neo4j/skills/
```

---

MIT License

Copyright (c) 2026 Neo4j Contrib

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
