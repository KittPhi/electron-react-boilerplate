<center>
<h1>Python Electron React: Boilerplate</h1>
<img src=https://miro.medium.com/max/3200/1*nBbb3oVqPH1g5Que9_VqbA.png alt="alt text" width="50%" height="50%">

[Tutorial Link](https://medium.com/heuristics/electron-react-python-part-3-boilerplate-1-3-45bbfa80fbe1)

<p>
<img src=./src/AakashMallik.png alt="alt text" width="20%" height="20%">
</p>

</center>

## Process:
> Electron Shell when launched will render http://localhost:3000
> (listens to the URL)

## 4 Major Parts:
---
<center>
<img src=https://miro.medium.com/max/2000/1*8Aa0EgH23jANgXdiJ-tU2A.png alt="alt text" width="40%" height="40%">
</center>

1. Main Procecss: creates and manages browser windows.
2. Render Process(visible): is created for each independent window (shows webpage).
3. Render Process(hidden): hidden process in another window (executes and closes)
4. Python Script: python-shell allows external python script to be executed from nodeJS application. Executed from inside the Hidden Process.
<center>
<img src=https://miro.medium.com/max/2000/1*e3qT-KDrnHjx2rdrKg55wQ.png alt="alt text" width="40%" height="40%">
</center>

## Commnunication:
1. Main - Renderer: both sides have have listeners to talk to one another.
<center>
<img src=https://miro.medium.com/max/1400/1*cp4CV-f8nAaPch1LIoT4SA.png alt="alt text" width="40%" height="40%">
</center>
2. Visible Renderer - Hidden Renderer: No direct communication, Main Process is the central hub (relay).
<center>
<img src=https://miro.medium.com/max/1400/1*iS4UIZtDvifJLZjaZcqkEQ.png alt="alt text" width="40%" height="40%">
</center>
1. Hidden Renderer - Python Script: **python-shell** makes use of *stdin* and *stdout* for sending and receiving data from the python script. **JSON** is the message format to be used.
<center>
<img src=https://miro.medium.com/max/1400/1*bVZQP1o5FENe3qhPhnqWbQ.png alt="alt text" width="40%" height="40%">
</center>

## Birds Eye View

<center>
<img src=https://miro.medium.com/max/2000/1*_SFcWW8nM74PHnNVxlH_Gw.png alt="alt text" width="40%" height="40%">
</center>

1. A function() in the *Visible Renderer Process* talks to the *Main Process* and asks for a *Hidden Renderer Process* to be run.
2. The *Main Process* has access to APIs that could create a new hidden browser window (*Hidden Renderer Process)*.
3. The *new hidden browser window* will make use of third-party library (*python-shell*) to execute a python script.
4. The output of the python script is then conveyed back to the *hidden browser window*.
5. The *hidden browser window* sends the data back to main process and the *Main Process* redirects it back to the original *Visible Renderer Process* that initiated the request for the user to see the final output.

<center>
<img src=https://miro.medium.com/max/2000/1*e3qT-KDrnHjx2rdrKg55wQ.png alt="alt text" width="40%" height="40%">
</center>

## Boiler Plate:
- Use **create-react-app** to develop a *React based UI* that runs in *electron shell*, while taking advantage of *python scritps* for heavy lifting.
  
```python
npm install -g create-react-app
create-react-app new_electron_project
npm install --save-dev electron
npm install --save-dev wait-on
npm install --save-dev concurrently
```
```
npm run react-start
```
In seperate terminal run:
```
npm run electron-start
```

```python
s = "Python syntax highlighting"
print s
```

```javascript
var s = "JavaScript syntax highlighting";
alert(s);
```

<center>
<img src=https://miro.medium.com/max/3200/1*nBbb3oVqPH1g5Que9_VqbA.png alt="alt text" width="50%" height="50%">
</center>