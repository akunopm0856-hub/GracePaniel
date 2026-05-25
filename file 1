const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;

app.use(express.json());
app.use(express.static('public'));

let bots = [];

app.get('/api/bots', (req, res) => {
    res.json(bots);
});

app.post('/api/bots', (req, res) => {
    const bot = {
        id: Date.now(),
        status: 'stopped',
        name: req.body.name,
        type: req.body.type,
        token: req.body.token
    };
    bots.push(bot);
    res.json(bot);
});

app.post('/api/bots/:id/start', (req, res) => {
    const bot = bots.find(b => b.id == parseInt(req.params.id));
    if (bot) bot.status = 'running';
    res.json({ status: 'started' });
});

app.post('/api/bots/:id/stop', (req, res) => {
    const bot = bots.find(b => b.id == parseInt(req.params.id));
    if (bot) bot.status = 'stopped';
    res.json({ status: 'stopped' });
});

app.delete('/api/bots/:id', (req, res) => {
    bots = bots.filter(b => b.id != parseInt(req.params.id));
    res.json({ deleted: true });
});

app.listen(PORT, () => {
    console.log(`🔥 BORN Panel running at http://localhost:${PORT}`);
});
