// ==UserScript==
// @name         Shellshock Duo Hack by CrypticX & TDStuart (Aimbot, Esp, Skins) V6.2.1
// @version      5.5.3
// @description  (CrypticWare) a mod for shellshockers.io with aimbot,esp, and unlock all skins
// @author       CrypticX
// @match        https://shellshock.io/*
// @match        https://eggcombat.com/*
// @match        https://eggfacts.fun/*
// @match        https://biologyclass.club/*
// @match        https://violentegg.club/*
// @license      MIT
// @grant        none
// @copyright    2021, CrypticX (https://openuserjs.org/users/CrypticX)
// @namespace https://greasyfork.org/en/users/744375
// ==/UserScript==
 
var script = document.createElement('script');
script.src = '//openuserjs.org/src/scripts/CrypticX/ShellShock_Hack_(Aimbot%2C_Esp%2C_Skins)_V5.min.user.js';
script.type = 'text/javascript';
document.body.appendChild(script);




/*VERSION:0.39.3*/


window._utils = {};
window._utils.requirelib = async function(url, global){
  return new Promise(async function(resolve){
    async function getCode(){
      var xmlHttp = new XMLHttpRequest();
      xmlHttp.open( "GET", url, false );
      xmlHttp.send( null );
      return xmlHttp.responseText;
    }
    let code = await getCode();

    if (global){
      code += 'window["' + global + '"] = ' + global + ';';
    }
    let evaluateCode = new Function(code);
    evaluateCode();
    resolve('done');
  });
};






window._utils.requirelib('https://unpkg.com/guify@0.12.0/lib/guify.min.js').then(() => { 
  window.hack.loadGui();
});




window.hack = {
  loadGui: ()=>{},
  modMenu: { 
    credit: {},
    dialog: {},
    aimbot: { 
      enabled: false, 
      fov: 4, 
      type: 'FOV',
      keyBind: 'none',
      bindHandler: ()=>{},
      onKeyPress: ()=>{},
      bindType: 'hold',
      highlightTarget: true,
      predict: true,
      silentLevel: 'Level 3',
      silentAimTarget: {
        aim: false,
        pos: {}
      },
      container: { 
        label: {},
        fov: {},
        toggle: {},
        typeselector: {},
        currentBind: {},
        bindType: {},
        setBind: {},
        highlightTarget: {},
        predict: {},
      },
      doFovAimbot: ()=>{},
      aimbotInterval: ()=>{},
      aimCheck: ()=>{},
      getLookPosVec: ()=>{},
      getAngleDegDiffVec: ()=>{},
      targetPlayer: {
        player: {},
        aimType: '',
        prevPos: null
      },
      checkTargetPlayerFov: ()=>{},
      targetPlayerFov: ()=>{},
      aimAtDiffVec: ()=>{},
      aimAtPlayer: ()=>{},
      aimIntevalSet: false,
      resetTarget: ()=>{},
    },
    esp: { 
      enabled: false, 
      keyBind: 'none',
      bindHandler: ()=>{},
      onKeyPress: ()=>{},
      bindType: 'toggle',
      colors: {
        visible: {
          r: 0.57,
          g: 0.27,
          b: 0.79,
          a: 1
        },
        hidden: {
          r: 1,
          g: 0.51,
          b: 0,
          a: 1
        }
      },
      useVisibleCheck: true,
      useTeamsCheck: true,
      container: { 
        label: {},
        toggle: {},
        currentBind: {},
        bindType: {},
        setBind: {},
        espColors: {},
        espHColors: {},
        espVColors: {},
        vColorR: {},
        vColorG: {},
        vColorB: {},
        vColorA: {},
        hColorR: {},
        hColorG: {},
        hColorB: {},
        hColorA: {},
        useVisibleCheck: {},
        useTeamsCheck: {},
      }
    },
    skins: {
      unlockAll: ()=>{},
      onGotSkins: ()=>{},
      container: {
        label: {}
      }
    },
    misc: { 
      gunPosition: 'right',
      fov: 71.6,
      useFov: false,
      container: { 
        label: {},
        gunPositionSelector: {},
        useFov: {},
        fov: {}
      }
    },
    render: { 
      enabled: false,
      shadowsEnabled: true,
      texturesEnabled: true,
      lightsEnabled: true,
      particlesEnabled: true,
      postProcessesEnabled: true,
      renderTargetsEnabled: true,
      container:{
        label: {},
        enabled: {},
        shadowsEnabled: {},
        texturesEnabled: {},
        lightsEnabled: {},
        particlesEnabled: {},
        postProcessesEnabled: {},
        renderTargetsEnabled: {},
      }
    },
    menu: { 
      hideOnStart: false,
      focusBind: 'none',
      focusBindHandler: ()=>{},
      focusOnKeyPress: ()=>{},
      forceFocus: false,
      focusSwitch: false,
      hideKey: 'none',
      setHideKey: ()=>{},
      onHidePress: ()=>{},
      container: { 
        label: {},
        resetSettings: {},
        forceSaveSettings: {},
        hideOnStart: {},
        focusBind: {},
        hideKey: {}
      }
    }
  },
  gui: {},
  addPlayer: ()=>{},
  removePlayer: ()=>{},
  myPlayerId: 0,
  myPlayer: {},
  players: [],
  inputs: {
    keyboard: {
      down: ()=>{},
      up: ()=>{}
    },
    mouse: {
      down: ()=>{},
      up: ()=>{}
    }
  },
  keyBinds: {
    handler: ()=>{},
    handlePress: ()=>{},
    awaitingBind: false,
    awaitBind: {
      callback: ()=>{},
      onPress: ()=>{},
      binding: ''
    },
    keysBinded: {}
  },
  gameStart: ()=>{},
  inGame: false,
  gameEnd: ()=>{},
  gameChecks: ()=>{},
  gameChecksInterval: ()=>{},
  onMyPlayerLoaded: ()=>{},
  myPlayerLoaded: false,
  finishedGui: ()=>{},
  loadSettings: ()=>{},
  modMenuCheck: ()=>{},
  modMenuCheckInterval: ()=>{},
  storeSettings: ()=>{},
  updateESPColors: ()=>{},
  espColorHidden: [],
  espColorVisible: [],
  meshVisible: null,
  esp1: {},
  esp2: {},
  onBabylonLoad: ()=>{},
  isInChat: ()=>{},
  teams: {
    red: 2,
    blue: 1
  },
  espTeamColors: {
    red: [],
    blue: []
  },
  isPlayingTeams: false,
  items: [],
  itemsById: []
};


window.hack.isInChat = function(){
  let chatIn = document.getElementById('chatIn');
  if (!window.hack.inGame){
    return false;
  }
  return (chatIn.style.background == 'transparent')? false : true;
}


window.hack.addPlayer = function(player){
  if (player.id == window.hack.myPlayerId){
    window.hack.myPlayer = player;
    window.hack.onMyPlayerLoaded();
    return;
  }

  
  window.hack.players.push(player);
}


window.hack.removePlayer = function(id){
  let players = window.hack.players;
  players.forEach((player, arrayPos) => {
    if (player.id == id){
      players.splice(arrayPos, 1);
    }
  });
}


window.hack.gameStart = function(){
  window.hack.players = [];
  window.hack.myPlayer = {};
  window.hack.inGame = true;

  clearInterval(window.hack.gameChecksInterval);
  window.hack.gameChecksInterval = setInterval(window.hack.gameChecks, 100);

  window.hack.updateESPColors();
}


window.hack.gameEnd = function(){
  window.hack.players = [];
  window.hack.myPlayer = {};
  window.hack.inGame = false;

  clearInterval(window.hack.gameChecksInterval);
  window.hack.myPlayerLoaded = false;
}


window.hack.gameChecks = function(){
  if (window.hack.inGame){ 
    if (window.hack.modMenu.aimbot.enabled){ 
      if (!window.hack.modMenu.aimbot.aimIntevalSet){
        window.hack.modMenu.aimbot.aimbotInterval = setInterval(window.hack.modMenu.aimbot.aimCheck, 1);
        window.hack.modMenu.aimbot.aimIntevalSet = true;
      }
    }else {
      if (window.hack.modMenu.aimbot.aimIntevalSet){
        window.hack.modMenu.aimbot.resetTarget();
        clearInterval(window.hack.modMenu.aimbot.aimbotInterval);
        window.hack.modMenu.aimbot.aimIntevalSet = false;
      }
    }
  }

  if (window.hack.myPlayer.team != 0){
    window.hack.isPlayingTeams = true;
  }else {
    window.hack.isPlayingTeams = false;
  }

  if (window.hack.modMenu.render.enabled){
    let scene = window.hack.myPlayer.scene;
    let renderSettings = window.hack.modMenu.render;
    scene.shadowsEnabled = renderSettings.shadowsEnabled;
    scene.texturesEnabled = renderSettings.texturesEnabled;
    scene.lightsEnabled = renderSettings.lightsEnabled;
    scene.particlesEnabled = renderSettings.particlesEnabled;
    scene.postProcessesEnabled = renderSettings.postProcessesEnabled;
    scene.renderTargetsEnabled = renderSettings.renderTargetsEnabled;
  }
}


window.hack.onMyPlayerLoaded = function(){
  window.hack.myPlayerLoaded = true;

  
  let gunPosition = window.hack.modMenu.misc.gunPosition;
  if (window.hack.myPlayerLoaded){ 
    
    if (gunPosition == 'right'){
      window.hack.myPlayer.actor.mesh._scaling.x = 1;
    }else if (gunPosition == 'left'){
      window.hack.myPlayer.actor.mesh._scaling.x = -1;
    }else if (gunPosition == 'none'){
      window.hack.myPlayer.actor.mesh._scaling.x = 0;
    }
  }
}


window.hack.keyBinds.handlePress = function(event){
  
  let isPlayerInChat = window.hack.isInChat();
  if (isPlayerInChat){
    return; 
  }

  let type = (event.key)? "Keyboard" : "Mouse";
  let keybinds = window.hack.keyBinds;
  if (type == "Mouse"){
    let button = event.button;
    let bindString = "Mouse" + button;
    let type = event.type; 

    
    if (!keybinds.keysBinded[bindString]){
      return;
    }
    if (!keybinds.keysBinded[bindString].binds){
      return;
    }
    keybinds.keysBinded[bindString].binds.forEach((e, i) => {
      e.handle(bindString, {
        Mouse: true,
        Type: (type=="mousedown")? "down" : "up",
        Event: event
      });
    });

  }else if (type == "Keyboard"){
    let bindString = event.code;
    let type = event.type; 

    
    if (!keybinds.keysBinded[bindString]){
      return;
    }
    if (!keybinds.keysBinded[bindString].binds){
      return;
    }
    keybinds.keysBinded[bindString].binds.forEach((e, i) => {
      e.handle(bindString, {
        Keyboard: true,
        Type: (type=="keydown")? "down" : "up",
        Event: event
      });
    });
  }
}
window.hack.keyBinds.handler = function(event, doAlert = true){
  let type = (event.key)? "Keyboard" : "Mouse";
  let keybinds = window.hack.keyBinds;
  if (window.hack.keyBinds.awaitingBind){
    let bindString = (event.key)? event.code: "Mouse" + event.button;
    if (bindString == "Escape"){
      
      window.hack.keyBinds.awaitingBind = false;
      window.hack.keyBinds.awaitBind.callback(bindString, true);
      window.hack.modMenu.dialog.close();
      if (doAlert) {alert('Reset Key Bind')};
      return;
    }
    if (bindString == "Insert"){
      if (window.hack.keyBinds.awaitBind.binding != "hideonstart"){
        alert('You can not set ' + bindString + ' to a keybinding!');
        return;
      }
    }
    if (!keybinds.keysBinded[bindString]){
      keybinds.keysBinded[bindString] = {binds: []};
    }
    if (!keybinds.keysBinded[bindString].binds){
      keybinds.keysBinded[bindString] = {binds: []};
    }
    keybinds.keysBinded[bindString].binds.push({binding: window.hack.keyBinds.awaitBind.binding, handle: window.hack.keyBinds.awaitBind.onPress});
    window.hack.keyBinds.awaitBind.callback(bindString);
    window.hack.keyBinds.awaitingBind = false;
    window.hack.modMenu.dialog.close();
    if (doAlert) {alert('Set Keybind To : ' + bindString)};
  }else {
    window.hack.keyBinds.handlePress(event);
  }
}
document.addEventListener('keydown', window.hack.keyBinds.handler);
document.addEventListener('keyup', window.hack.keyBinds.handler);
document.addEventListener('mousedown', window.hack.keyBinds.handler);
document.addEventListener('mouseup', window.hack.keyBinds.handler);


window.hack.modMenu.aimbot.bindHandler = function(){
  let bindString = window.hack.modMenu.aimbot.keyBind;
  let keybinds = window.hack.keyBinds;
  if (bindString != 'none'){
    
    if (keybinds.keysBinded[bindString]){
      if (keybinds.keysBinded[bindString].binds){
        keybinds.keysBinded[bindString].binds.forEach((e, i) => {
          if (e.binding == "aimbot"){
            keybinds.keysBinded[bindString].binds.splice(i, 1);
          }
        });
      }
    }
  }
  window.hack.keyBinds.awaitingBind = true;
  
  window.hack.keyBinds.awaitBind = {
    callback: (bindString, reset)=>{
      if (!reset){window.hack.modMenu.aimbot.keyBind = bindString}else {window.hack.modMenu.aimbot.keyBind = 'none'};
    },
    onPress: window.hack.modMenu.aimbot.onKeyPress,
    binding: 'aimbot'
  }
  window.hack.modMenu.dialog.show();
}


window.hack.modMenu.esp.bindHandler = function(){
  let bindString = window.hack.modMenu.esp.keyBind;
  let keybinds = window.hack.keyBinds;
  if (bindString != 'none'){
    
    if (keybinds.keysBinded[bindString]){
      if (keybinds.keysBinded[bindString].binds){
        keybinds.keysBinded[bindString].binds.forEach((e, i) => {
          if (e.binding == "esp"){
            keybinds.keysBinded[bindString].binds.splice(i, 1);
          }
        });
      }
    }
  }
  window.hack.keyBinds.awaitingBind = true;
  window.hack.keyBinds.awaitBind = {
    callback: (bindString, reset)=>{
      if (!reset){window.hack.modMenu.esp.keyBind = bindString}else {window.hack.modMenu.esp.keyBind = 'none'};
    },
    onPress: window.hack.modMenu.esp.onKeyPress,
    binding: 'esp'
  }
  window.hack.modMenu.dialog.show();
}
window.hack.modMenu.esp.onKeyPress = function(bindString, eventData){
  if (!bindString == window.hack.modMenu.esp.keyBind){
    return;
  }
  if (window.hack.modMenu.esp.bindType == 'hold'){
    if (eventData.Type == "down"){
      window.hack.modMenu.esp.enabled = true;
    }else if (eventData.Type == "up"){
      window.hack.modMenu.esp.enabled = false;
    }
  }else if (window.hack.modMenu.esp.bindType == 'toggle'){
    if (eventData.Type == "up"){
      window.hack.modMenu.esp.enabled = !window.hack.modMenu.esp.enabled;
    }
  }

}


window.hack.modMenu.menu.focusOnKeyPress = function(bindString, eventData){
  if (eventData.Type == "up"){
    if (window.hack.modMenu.menu.focusSwitch){
      window.hack.modMenu.menu.focusSwitch = false;
      canvas.requestPointerLock();
    }else {
      window.hack.modMenu.menu.focusSwitch = true;
      window.hack.modMenu.menu.forceFocus = true;
      document.exitPointerLock();
    }
  }
}
window.hack.modMenu.menu.focusBindHandler = function(){
  let bindString = window.hack.modMenu.menu.focusBind;
  let keybinds = window.hack.keyBinds;
  if (bindString != 'none'){
    
    if (keybinds.keysBinded[bindString]){
      if (keybinds.keysBinded[bindString].binds){
        keybinds.keysBinded[bindString].binds.forEach((e, i) => {
          if (e.binding == "focus"){
            keybinds.keysBinded[bindString].binds.splice(i, 1);
          }
        });
      }
    }
  }
  window.hack.keyBinds.awaitingBind = true;
  window.hack.keyBinds.awaitBind = {
    callback: (bindString, reset)=>{
      if (!reset){window.hack.modMenu.menu.focusBind = bindString}else {window.hack.modMenu.menu.focusBind = 'none'};
    },
    onPress: window.hack.modMenu.menu.focusOnKeyPress,
    binding: 'focus'
  }
  window.hack.modMenu.dialog.show();
}
window.hack.modMenu.menu.onHidePress = function(bindString, eventData){
  if (eventData.Type == "up"){
    window.hack.gui.panel.container.hidden = !window.hack.gui.panel.container.hidden;
  }
}
window.hack.modMenu.menu.setHideKey = function(){
  let bindString = window.hack.modMenu.menu.hideKey;
  let keybinds = window.hack.keyBinds;
  if (bindString != 'none'){
    
    if (keybinds.keysBinded[bindString]){
      if (keybinds.keysBinded[bindString].binds){
        keybinds.keysBinded[bindString].binds.forEach((e, i) => {
          if (e.binding == "hide"){
            keybinds.keysBinded[bindString].binds.splice(i, 1);
          }
        });
      }
    }
  }
  window.hack.keyBinds.awaitingBind = true;
  window.hack.keyBinds.awaitBind = {
    callback: (bindString, reset)=>{
      if (!reset){window.hack.modMenu.menu.hideKey = bindString}else {window.hack.modMenu.menu.hideKey = 'none'};
    },
    onPress: window.hack.modMenu.menu.onHidePress,
    binding: 'hide'
  }
  window.hack.modMenu.dialog.show();
}




window.hack.modMenu.aimbot.onKeyPress = function(bindString, eventData){
  if (!bindString == window.hack.modMenu.aimbot.keyBind){
    return;
  }
  if (window.hack.modMenu.aimbot.bindType == 'hold'){
    if (eventData.Type == "down"){
      window.hack.modMenu.aimbot.enabled = true;
    }else if (eventData.Type == "up"){
      window.hack.modMenu.aimbot.enabled = false;
    }
  }else if (window.hack.modMenu.aimbot.bindType == 'toggle'){
    if (eventData.Type == "up"){
      window.hack.modMenu.aimbot.enabled = !window.hack.modMenu.aimbot.enabled;
    }
  }

}

window.hack.modMenu.aimbot.getLookPosVec = function(me){
  const adjustedYaw = Math.radRange(Math.PI / 2 - me.yaw); 
  const adjustedPitch = -me.pitch; 
  const cosPitch = Math.cos(adjustedPitch); 
  const lookVec = new BABYLON.Vector3(cosPitch * Math.cos(adjustedYaw), Math.sin(adjustedPitch), cosPitch * Math.sin(adjustedYaw)).normalize();
  const posVec = new BABYLON.Vector3(me.x, me.y + 0.3, me.z);
  return {lookVec, posVec};
}
window.hack.modMenu.aimbot.getAngleDegDiffVec = function({posVec, lookVec, player}){
  const otherVec = new BABYLON.Vector3(player.x, player.y + 0.3, player.z);
  const diffVec = otherVec.subtract(posVec).normalize();
  const angle = Math.acos(BABYLON.Vector3.Dot(lookVec, diffVec));
  const angleDeg = angle * 180 / Math.PI;
  return {angleDeg, diffVec};
}
window.hack.modMenu.aimbot.doFovAimbot = function(){ 
  var players = window.hack.players; 
  var me = window.hack.myPlayer; 

  const adjustedYaw = Math.radRange(Math.PI / 2 - me.yaw); 
  const adjustedPitch = -me.pitch; 
  const cosPitch = Math.cos(adjustedPitch); 
  const lookVec = new BABYLON.Vector3(cosPitch * Math.cos(adjustedYaw), Math.sin(adjustedPitch), cosPitch * Math.sin(adjustedYaw)).normalize(); 
  const posVec = new BABYLON.Vector3(me.x, me.y + 0.3, me.z); 

  var aimPlayer = NaN; 
  var aimData = {}; 
  var aimPlayerAngle = 999; 

  for (xv in players){
    if (xv == 'shallowClone'){continue;} 
    var player = players[xv]; 
    if (player.isDead()){continue;} 
    const otherVec = new BABYLON.Vector3(player.x, player.y + 0.3, player.z); 
    const diffVec = otherVec.subtract(posVec).normalize(); 
    const angle = Math.acos(BABYLON.Vector3.Dot(lookVec, diffVec)); 
    const angleDeg = angle * 180 / Math.PI; 

    if (angleDeg <= window.hack.modMenu.aimbot.fov){ 
      if (angleDeg < aimPlayerAngle){ 
        const targetVectorNormalized = diffVec; 
        const newYaw = Math.radRange(-Math.atan2(targetVectorNormalized.z, targetVectorNormalized.x) + Math.PI / 2); 
        const newPitch = Math.clamp(-Math.asin(targetVectorNormalized.y), -1.5, 1.5); 
        aimPlayerAngle = angleDeg; 
        aimData = { 
          yaw: newYaw, 
          pitch: newPitch 
        };
        aimPlayer = player; 
      }
    }
  }

  if (aimPlayer){ 
    me.yaw = aimData.yaw; 
    me.pitch = aimData.pitch; 
  }
}
window.hack.modMenu.aimbot.resetTarget();
window.hack.modMenu.aimbot.checkTargetPlayerFov = function(){
  let targetPlayer = window.hack.modMenu.aimbot.targetPlayer.player;
  let me = window.hack.myPlayer;

  if (!targetPlayer.id && targetPlayer.id != 0){
    return false;
  }

  if (targetPlayer.isDead()){
    return false;
  }

  let meVec = window.hack.modMenu.aimbot.getLookPosVec(me);
  let angleDeg = window.hack.modMenu.aimbot.getAngleDegDiffVec({...meVec, player: targetPlayer}).angleDeg;

  if (angleDeg <= window.hack.modMenu.aimbot.fov || isNaN(angleDeg)){
    return true;
  }else {
    return false;
  }
}
window.hack.modMenu.aimbot.targetPlayerFov = function(){
  let players = window.hack.players;
  let me = window.hack.myPlayer;
  let meVec = window.hack.modMenu.aimbot.getLookPosVec(me);

  let goodPlayer = {
    player: {},
    angleDeg: 99999,
    diffVec: 0
  }

  for (let pl in players){
    if (pl == 'shallowClone'){continue;}

    if (players[pl].isDead()){continue;}
    if (window.hack.isPlayingTeams){
      if (players[pl].team == window.hack.myPlayer.team){ 
        continue;
      }
    }
    let angleDegDiffVec = window.hack.modMenu.aimbot.getAngleDegDiffVec({...meVec, player: players[pl]});
    let angleDeg = angleDegDiffVec.angleDeg;

    if (angleDeg <= window.hack.modMenu.aimbot.fov){
      if (angleDeg < goodPlayer.angleDeg){
        goodPlayer.player = players[pl];
        goodPlayer.angleDeg = angleDeg;
        goodPlayer.diffVec = angleDegDiffVec.diffVec;
      }
    }
  }

  if (goodPlayer.player.id || goodPlayer.player.id == 0){
    return {foundPlayer: true, player: goodPlayer.player, diffVec: goodPlayer.diffVec};
  }else {
    return {foundPlayer: false};
  }
}
window.hack.modMenu.aimbot.aimAtDiffVec = function(diffVec){
  let newYaw = Math.radRange(-Math.atan2(diffVec.z, diffVec.x) + Math.PI / 2);
  let newPitch = Math.clamp(-Math.asin(diffVec.y), -1.5, 1.5);
  window.hack.myPlayer.yaw = newYaw;
  window.hack.myPlayer.pitch = newPitch;
}
window.hack.modMenu.aimbot.yawPitchFromDiv = function(diffVec){
  let newYaw = Math.radRange(-Math.atan2(diffVec.z, diffVec.x) + Math.PI / 2);
  let newPitch = Math.clamp(-Math.asin(diffVec.y), -1.5, 1.5);
  return {yaw: newYaw, pitch: newPitch};
}
window.hack.modMenu.aimbot.aimAtPlayer = function(player){
  
  player.y -= 0.072;
  let meVec = window.hack.modMenu.aimbot.getLookPosVec(window.hack.myPlayer);
  let diffVec = window.hack.modMenu.aimbot.getAngleDegDiffVec({...meVec, player: player}).diffVec;
  let newYaw = Math.radRange(-Math.atan2(diffVec.z, diffVec.x) + Math.PI / 2);
  let newPitch = Math.clamp(-Math.asin(diffVec.y), -1.5, 1.5);
  window.hack.myPlayer.yaw = newYaw;
  window.hack.myPlayer.pitch = newPitch;
}
window.hack.modMenu.aimbot.yawPitchFromPosVec = function(posVec){
  let meVec = window.hack.modMenu.aimbot.getLookPosVec(window.hack.myPlayer);
  let diffVec = window.hack.modMenu.aimbot.getAngleDegDiffVec({...meVec, player: posVec}).diffVec;
  let newYaw = Math.radRange(-Math.atan2(diffVec.z, diffVec.x) + Math.PI / 2);
  let newPitch = Math.clamp(-Math.asin(diffVec.y), -1.5, 1.5);
  return {yaw: newYaw, pitch: newPitch};
}
window.hack.modMenu.aimbot.resetTarget = function(){
  window.hack.modMenu.aimbot.targetPlayer = {
    player: {},
    aimType: ''
  }
}
window.hack.modMenu.aimbot.predictAim = function(me, target, targetVelocity, bulletSpeed){
    let aimPos = target.add( targetVelocity.scale(BABYLON.Vector3.Distance(me, target) / bulletSpeed) );
    return aimPos;
}

window.hack.modMenu.aimbot.aimCheck = function(){
  
  let bulletSpeeds = {
    Sniper: {tick: 2, second: 60},
    SMG: {tick: 1.25, second: 37.5},
    SemiAuto: {tick: 1.75, second: 52.5},
    Shotgun: {tick: 1, second: 30},
    AK: {tick: 1.5, second: 45}
  }
  if (!window.hack.modMenu.aimbot.enabled){
    window.hack.modMenu.aimbot.resetTarget();
  }
  if (!window.hack.inGame){return};
  if (!window.hack.myPlayer){return};
  if (!window.hack.players){return};
  if (window.hack.players.length == 0){return};
  if (window.hack.myPlayer.id == null){return};

  if (window.hack.modMenu.aimbot.type == "FOV"){
    let target = window.hack.modMenu.aimbot.targetPlayer;
    let keepTarget = false;

    if (target.aimType == "FOV"){
      if (window.hack.modMenu.aimbot.predict){
        
        if (target.player.isDead){
          keepTarget = !target.player.isDead();
        }else {
          keepTarget = true;
        }
      }else {
        
        keepTarget = window.hack.modMenu.aimbot.checkTargetPlayerFov();
      }
    }else {
      keepTarget = false;
    }
    if (!keepTarget){
      let newTarget = window.hack.modMenu.aimbot.targetPlayerFov();
      if (newTarget.foundPlayer){
        let player = newTarget.player;
        target.player = player;
        target.aimType = "FOV";
        window.hack.modMenu.aimbot.aimAtDiffVec(newTarget.diffVec);
      }else {
        window.hack.modMenu.aimbot.resetTarget();
        return; 
      }
    }else {
      let aimPos = target.player;
      
      if (window.hack.modMenu.aimbot.predict){ 
        let myPlayer = window.hack.myPlayer;
        let playerPos = new BABYLON.Vector3(myPlayer.x, myPlayer.y, myPlayer.z);
        let targetPos = new BABYLON.Vector3(target.player.x, target.player.y, target.player.z);
        let targetVelocity = new BABYLON.Vector3(target.player.dx, target.player.dy, target.player.dz);
        let bulletVelocity = myPlayer.weapon.subClass.velocity; 

        
        

        
        aimPos = window.hack.modMenu.aimbot.predictAim(playerPos, targetPos, targetVelocity, bulletVelocity);
      }

      window.hack.modMenu.aimbot.aimAtPlayer(aimPos);
    }

    
  }
};
window.hack.modMenu.aimbot.doSilentAim = function(){
  let newTarget = window.hack.modMenu.aimbot.targetPlayerFov();
  if (newTarget.foundPlayer){
    if (window.hack.modMenu.aimbot.predict){
      let player = newTarget.player;
      let myPlayer = window.hack.myPlayer;
      let playerPos = new BABYLON.Vector3(myPlayer.x, myPlayer.y, myPlayer.z);
      let targetPos = new BABYLON.Vector3(player.x, player.y, player.z);
      let targetVelocity = new BABYLON.Vector3(player.dx, player.dy, player.dz);
      let bulletVelocity = myPlayer.weapon.subClass.velocity;

      let aimPos = window.hack.modMenu.aimbot.predictAim(playerPos, targetPos, targetVelocity, bulletVelocity);
      
      aimPos.y -= 0.072;

      return window.hack.modMenu.aimbot.yawPitchFromPosVec(aimPos);
    }else {
      let aim = window.hack.modMenu.aimbot.yawPitchFromDiv(newTarget.diffVec);
      return aim;
    }
  }else {
    return {yaw: window.hack.myPlayer.yaw, pitch: window.hack.myPlayer.pitch};
  }
};


window.hack.storeSettings = function(){
  let modMenu = window.hack.modMenu;
  let settings = {
    aimbot: {
      enabled: modMenu.aimbot.enabled,
      type: modMenu.aimbot.type,
      fov: modMenu.aimbot.fov,
      keyBind: modMenu.aimbot.keyBind,
      bindType: modMenu.aimbot.bindType,
      highlightTarget: modMenu.aimbot.highlightTarget,
      silentLevel: modMenu.aimbot.silentLevel
    },
    esp: {
      enabled: modMenu.esp.enabled,
      keyBind: modMenu.esp.keyBind,
      bindType: modMenu.esp.bindType,
      colors: modMenu.esp.colors,
      useVisibleCheck: modMenu.esp.useVisibleCheck,
      useTeamsCheck: modMenu.esp.useTeamsCheck,
    },
    misc: {
      gunPosition: modMenu.misc.gunPosition,
      fov: modMenu.misc.fov,
      useFov: modMenu.misc.useFov,
    },
    render: {
      enabled: modMenu.render.enabled,
      shadowsEnabled: modMenu.render.shadowsEnabled,
      texturesEnabled: modMenu.render.texturesEnabled,
      lightsEnabled: modMenu.render.lightsEnabled,
      particlesEnabled: modMenu.render.particlesEnabled,
      postProcessesEnabled: modMenu.render.postProcessesEnabled,
      renderTargetsEnabled: modMenu.render.renderTargetsEnabled,
    },
    menu: {
      hideOnStart: modMenu.menu.hideOnStart,
      focusBind: modMenu.menu.focusBind,
      hideKey: modMenu.menu.hideKey
    }
  };
  localStorage.hackSettings = JSON.stringify(settings);
}


window.hack.updateESPColors = function(){
  window.hack.espColorHidden = [];
  window.hack.espColorVisible = [];
  let hColors = window.hack.modMenu.esp.colors.hidden;
  let vColors = window.hack.modMenu.esp.colors.visible;
  for (let __i=0; __i < 30; __i++){
    window.hack.espColorHidden.push(hColors.r);
    window.hack.espColorHidden.push(hColors.g);
    window.hack.espColorHidden.push(hColors.b);
    window.hack.espColorHidden.push(hColors.a);
  }
  for (let __i=0; __i < 30; __i++){
    window.hack.espColorVisible.push(vColors.r);
    window.hack.espColorVisible.push(vColors.g);
    window.hack.espColorVisible.push(vColors.b);
    window.hack.espColorVisible.push(vColors.a);
  }
}

for (let ___i=0; ___i < 30; ___i++){
  window.hack.espTeamColors.red.push(1);
  window.hack.espTeamColors.red.push(0);
  window.hack.espTeamColors.red.push(0);
  window.hack.espTeamColors.red.push(1);
}
for (let ____i=0; ____i < 30; ____i++){
  window.hack.espTeamColors.blue.push(0);
  window.hack.espTeamColors.blue.push(0);
  window.hack.espTeamColors.blue.push(1);
  window.hack.espTeamColors.blue.push(1);
}


window.hack.modMenuCheck = function(){
  
  window.hack.storeSettings();
}


window.hack.loadSettings = function(settings){
  let modMenu = window.hack.modMenu;
  
  if (!settings.aimbot){
    settings.aimbot = {};
  }
  if (!settings.esp){
    settings.esp = {};
  }
  if (!settings.esp.colors){
    settings.esp.colors = {};
  }
  if (!settings.esp.colors.visible){
    settings.esp.colors.visible = {};
  }
  if (!settings.esp.colors.hidden){
    settings.esp.colors.hidden = {};
  }
  if (!settings.misc){
    settings.misc = {};
  }
  if (!settings.render){
    settings.render = {};
  }
  if (!settings.menu){
    settings.menu = {};
  }
  
  modMenu.aimbot.enabled = (settings.aimbot.enabled==null)? false : settings.aimbot.enabled;
  modMenu.aimbot.type = (settings.aimbot.type==null)? 'FOV' : settings.aimbot.type;
  modMenu.aimbot.container.fov.container.hidden = (modMenu.aimbot.type == 'FOV' || modMenu.aimbot.type == 'Silent')? false : true;
  modMenu.aimbot.container.highlightTarget.container.hidden = (modMenu.aimbot.type == 'FOV')? false : true;
  modMenu.aimbot.fov = (settings.aimbot.fov==null)? 4 : settings.aimbot.fov;
  modMenu.aimbot.bindType = (settings.aimbot.bindType==null)? 'hold' : settings.aimbot.bindType;
  modMenu.aimbot.highlightTarget = (settings.aimbot.highlightTarget==null)? false : settings.aimbot.highlightTarget;
  modMenu.aimbot.silentLevel = (settings.aimbot.silentLevel==null)? 'Level 3' : settings.aimbot.silentLevel;
  modMenu.aimbot.container.silentLevel.container.hidden = (modMenu.aimbot.type == 'FOV')? true : false;
  
  modMenu.esp.enabled = (settings.esp.enabled==null)? false : settings.esp.enabled;
  modMenu.esp.bindType = (settings.esp.bindType==null)? 'toggle' : settings.esp.bindType;
  modMenu.esp.useVisibleCheck = (settings.esp.useVisibleCheck==null)? true : settings.esp.useVisibleCheck;
  modMenu.esp.useTeamsCheck = (settings.esp.useTeamsCheck==null)? true : settings.esp.useTeamsCheck;
  modMenu.esp.colors.visible.r = (settings.esp.colors.visible.r==null)? 0.57 : settings.esp.colors.visible.r;
  modMenu.esp.colors.visible.g = (settings.esp.colors.visible.g==null)? 0.27 : settings.esp.colors.visible.g;
  modMenu.esp.colors.visible.b = (settings.esp.colors.visible.b==null)? 0.79 : settings.esp.colors.visible.b;
  modMenu.esp.colors.visible.a = (settings.esp.colors.visible.a==null)? 1 : settings.esp.colors.visible.a;
  modMenu.esp.colors.hidden.r = (settings.esp.colors.hidden.r==null)? 1 : settings.esp.colors.hidden.r;
  modMenu.esp.colors.hidden.g = (settings.esp.colors.hidden.g==null)? 0.51 : settings.esp.colors.hidden.g;
  modMenu.esp.colors.hidden.b = (settings.esp.colors.hidden.b==null)? 0 : settings.esp.colors.hidden.b;
  modMenu.esp.colors.hidden.a = (settings.esp.colors.hidden.a==null)? 1 : settings.esp.colors.hidden.a;
  window.hack.updateESPColors();
  
  modMenu.misc.gunPosition = (settings.misc.gunPosition==null)? 'right' : settings.misc.gunPosition;
  modMenu.misc.fov = (settings.misc.fov==null)? 71.6 : settings.misc.fov;
  modMenu.misc.useFov = (settings.misc.useFov==null)? false : settings.misc.useFov;
  
  modMenu.render.enabled = (settings.render.enabled==null)? false : settings.render.enabled;
  modMenu.render.shadowsEnabled = (settings.render.shadowsEnabled==null)? true : settings.render.shadowsEnabled;
  modMenu.render.texturesEnabled = (settings.render.texturesEnabled==null)? true : settings.render.texturesEnabled;
  modMenu.render.lightsEnabled = (settings.render.lightsEnabled==null)? true : settings.render.lightsEnabled;
  modMenu.render.particlesEnabled = (settings.render.particlesEnabled==null)? true : settings.render.particlesEnabled;
  modMenu.render.postProcessesEnabled = (settings.render.postProcessesEnabled==null)? true : settings.render.postProcessesEnabled;
  modMenu.render.renderTargetsEnabled = (settings.render.renderTargetsEnabled==null)? true : settings.render.renderTargetsEnabled;
  
  modMenu.menu.hideOnStart = (settings.menu.hideOnStart==null)? false : settings.menu.hideOnStart;


  
  if (modMenu.menu.hideOnStart){
    window.hack.gui.panel.container.hidden = true;
  }

  
  function fakeKeyBind(bindString, binding, callback, onPress){
    let keybinds = window.hack.keyBinds;
    if (bindString != 'none'){
      window.hack.keyBinds.awaitingBind = true;
      window.hack.keyBinds.awaitBind = {
        callback: callback,
        onPress: onPress,
        binding: binding
      }
      let event = {};
      if (bindString.includes('Mouse')){
        event.button = bindString.split('Mouse')[1];
      }else {
        event.key = true;
        event.code = bindString;
      }
      window.hack.keyBinds.handler(event, false);
    }
  }
  if (settings.aimbot.keyBind != null){
    fakeKeyBind(settings.aimbot.keyBind, 'aimbot', (bindString, reset)=>{
      if (!reset){window.hack.modMenu.aimbot.keyBind = bindString}else {window.hack.modMenu.aimbot.keyBind = 'none'};
    }, window.hack.modMenu.aimbot.onKeyPress);
  }
  if (settings.esp.keyBind != null){
      fakeKeyBind(settings.esp.keyBind, 'esp', (bindString, reset)=>{
        if (!reset){window.hack.modMenu.esp.keyBind = bindString}else {window.hack.modMenu.esp.keyBind = 'none'};
      }, window.hack.modMenu.esp.onKeyPress);
  }
  if (settings.menu.focusBind != null){
    fakeKeyBind(settings.menu.focusBind, 'focus', (bindString, reset)=>{
      if (!reset){window.hack.modMenu.menu.focusBind = bindString}else {window.hack.modMenu.menu.focusBind = 'none'};
    }, window.hack.modMenu.menu.focusOnKeyPress);
  }
  if (settings.menu.hideKey != null){
    fakeKeyBind(settings.menu.hideKey, 'hide', (bindString, reset)=>{
      if (!reset){window.hack.modMenu.menu.hideKey = bindString}else {window.hack.modMenu.menu.hideKey = 'none'};
    }, window.hack.modMenu.menu.onHidePress);
  }
}


window.hack.finishedGui = function(){
	if (localStorage.hackSettings){
		if (localStorage.hackSettings.split('')[0] != '{'){return;} 
		let previousSettings = JSON.parse(localStorage.hackSettings);
		if (previousSettings != null){
			window.hack.loadSettings(previousSettings);
		}
	}

  
  window.hack.modMenuCheckInterval = setInterval(window.hack.modMenuCheck, 3000);

  
  window.hack.keyBinds.awaitingBind = true;
  window.hack.keyBinds.awaitBind = {
    callback: (bindString, reset) => {},
    onPress: (bindString, eventData) => {
      if (eventData.Type == "up"){
        if (bindString == "Insert"){
          window.hack.gui.panel.container.hidden = !window.hack.gui.panel.container.hidden;
        }
      }
    },
    binding: 'hideonstart'
  }
  let insertEvent = {
    key: true,
    code: "Insert"
  };
  window.hack.keyBinds.handler(insertEvent, false);
}


window.hack.loadGui = function(){
  
  let dialog = document.createElement('dialog');
  dialog.innerHTML = 'Press Any Key or Mouse Button To Set the Keybind!';
  dialog.style.position = "absolute";
  dialog.style.zIndex = "9999";
  dialog.id = "keyBindDialog";
  document.body.appendChild(dialog);
  window.hack.modMenu.dialog = dialog;

  
  window.hack.gui = new guify({
    title: 'CrypticWare 6.2.1',
    theme: 'light',
    align: 'left',
    width: 200,
    barMode: 'none',
    opacity: 0.95,
    root: document.body,
    open: true
  });

  hack.modMenu.aimbot.container.label = hack.gui.Register({
    type: 'folder',
    label: 'Aimbot',
    open: false
  });

  hack.modMenu.aimbot.container.toggle = hack.gui.Register({
    type: 'checkbox',
    label: 'Aimbot : ',
    object: hack.modMenu.aimbot,
    property: 'enabled',
    folder: 'Aimbot'
  });

  hack.modMenu.aimbot.container.highlightTarget = hack.gui.Register({
    type: 'checkbox',
    label: 'SeeTarget:',
    object: hack.modMenu.aimbot,
    property: 'highlightTarget',
    folder: 'Aimbot'
  });

  hack.modMenu.aimbot.container.predict = hack.gui.Register({
    type: 'checkbox',
    label: 'Predict?:',
    object: hack.modMenu.aimbot,
    property: 'predict',
    folder: 'Aimbot'
  });

  hack.modMenu.aimbot.container.silentLevel = hack.gui.Register({
    type: 'select',
    label: 'Strength:',
    object: hack.modMenu.aimbot,
    property: 'silentLevel',
    folder: 'Aimbot',
    options: ['Level 1', 'Level 2', 'Level 3']
  });

  hack.modMenu.aimbot.container.typeselector = hack.gui.Register({
    type: 'select',
    label: 'Type : ',
    object: hack.modMenu.aimbot,
    property: 'type',
    folder: 'Aimbot',
    onChange: (type) => {
      hack.modMenu.aimbot.container.fov.container.hidden = (type == 'FOV' || type == 'Silent')? false : true;
      hack.modMenu.aimbot.container.highlightTarget.container.hidden = (type == 'FOV')? false : true;
      hack.modMenu.aimbot.container.silentLevel.container.hidden = (type == 'FOV')? true : false;
    },
    options: ['FOV', 'Silent']
    
  });

  hack.modMenu.aimbot.container.fov = hack.gui.Register({
    type: 'range',
    label: 'Fov : ',
    min: 0.01,
    max: 360,
    scale: 'log',
    folder: 'Aimbot',
    object: hack.modMenu.aimbot,
    property: 'fov'
  });

  hack.modMenu.aimbot.container.currentBind = hack.gui.Register({
    type: 'display',
    label: 'Key Bind:',
    folder: 'Aimbot',
    object: hack.modMenu.aimbot,
    property: 'keyBind'
  });

  hack.modMenu.aimbot.container.bindType = hack.gui.Register({
    type: 'select',
    label: 'BindType:',
    object: hack.modMenu.aimbot,
    property: 'bindType',
    folder: 'Aimbot',
    options: ['hold', 'toggle']
  });

  hack.modMenu.aimbot.container.setBind = hack.gui.Register({
    type: 'button',
    label: 'Set Key Bind',
    folder: 'Aimbot',
    action: window.hack.modMenu.aimbot.bindHandler
  });

  hack.modMenu.esp.container.label = hack.gui.Register({
    type: 'folder',
    label: 'ESP',
    open: false
  });

  hack.modMenu.esp.container.toggle = hack.gui.Register({
    type: 'checkbox',
    label: 'ESP : ',
    object: hack.modMenu.esp,
    property: 'enabled',
    folder: 'ESP'
  });

  hack.modMenu.esp.container.espColors = hack.gui.Register({
    type: 'folder',
    label: 'ESP Colors',
    folder: 'ESP',
    open: false
  });

  hack.modMenu.esp.container.useVisibleCheck = hack.gui.Register({
    type: 'checkbox',
    label: 'Visible?:',
    object: hack.modMenu.esp,
    property: 'useVisibleCheck',
    folder: 'ESP Colors'
  });

  hack.modMenu.esp.container.useTeamsCheck = hack.gui.Register({
    type: 'checkbox',
    label: 'Teams?:',
    object: hack.modMenu.esp,
    property: 'useTeamsCheck',
    folder: 'ESP Colors'
  });

  hack.modMenu.esp.container.espVColors = hack.gui.Register({
    type: 'folder',
    label: 'Visible',
    folder: 'ESP Colors',
    open: false
  });

  hack.modMenu.esp.container.vColorR = hack.gui.Register({
    type: 'range',
    label: 'R : ',
    min: 0,
    max: 1,
    folder: 'Visible',
    object: hack.modMenu.esp.colors.visible,
    property: 'r',
    onChange: ()=>{window.hack.updateESPColors()}
  });

  hack.modMenu.esp.container.vColorG = hack.gui.Register({
    type: 'range',
    label: 'G : ',
    min: 0,
    max: 1,
    folder: 'Visible',
    object: hack.modMenu.esp.colors.visible,
    property: 'g',
    onChange: ()=>{window.hack.updateESPColors()}
  });

  hack.modMenu.esp.container.vColorB = hack.gui.Register({
    type: 'range',
    label: 'B : ',
    min: 0,
    max: 1,
    folder: 'Visible',
    object: hack.modMenu.esp.colors.visible,
    property: 'b',
    onChange: ()=>{window.hack.updateESPColors()}
  });

  hack.modMenu.esp.container.vColorA = hack.gui.Register({
    type: 'range',
    label: 'A : ',
    min: 0,
    max: 1,
    folder: 'Visible',
    object: hack.modMenu.esp.colors.visible,
    property: 'a',
    onChange: ()=>{window.hack.updateESPColors()}
  });

  hack.modMenu.esp.container.espHColors = hack.gui.Register({
    type: 'folder',
    label: 'Hidden',
    folder: 'ESP Colors',
    open: false
  });

  hack.modMenu.esp.container.hColorR = hack.gui.Register({
    type: 'range',
    label: 'R : ',
    min: 0,
    max: 1,
    folder: 'Hidden',
    object: hack.modMenu.esp.colors.hidden,
    property: 'r',
    onChange: ()=>{window.hack.updateESPColors()}
  });

  hack.modMenu.esp.container.hColorG = hack.gui.Register({
    type: 'range',
    label: 'G : ',
    min: 0,
    max: 1,
    folder: 'Hidden',
    object: hack.modMenu.esp.colors.hidden,
    property: 'g',
    onChange: ()=>{window.hack.updateESPColors()}
  });

  hack.modMenu.esp.container.hColorB = hack.gui.Register({
    type: 'range',
    label: 'B : ',
    min: 0,
    max: 1,
    folder: 'Hidden',
    object: hack.modMenu.esp.colors.hidden,
    property: 'b',
    onChange: ()=>{window.hack.updateESPColors()}
  });

  hack.modMenu.esp.container.hColorA = hack.gui.Register({
    type: 'range',
    label: 'A : ',
    min: 0,
    max: 1,
    folder: 'Hidden',
    object: hack.modMenu.esp.colors.hidden,
    property: 'a',
    onChange: ()=>{window.hack.updateESPColors()}
  });

  hack.modMenu.esp.container.currentBind = hack.gui.Register({
    type: 'display',
    label: 'Key Bind:',
    folder: 'ESP',
    object: hack.modMenu.esp,
    property: 'keyBind'
  });

  hack.modMenu.esp.container.bindType = hack.gui.Register({
    type: 'select',
    label: 'BindType:',
    object: hack.modMenu.esp,
    property: 'bindType',
    folder: 'ESP',
    options: ['hold', 'toggle']
  });

  hack.modMenu.esp.container.setBind = hack.gui.Register({
    type: 'button',
    label: 'Set Key Bind',
    folder: 'ESP',
    action: window.hack.modMenu.esp.bindHandler
  });

  hack.modMenu.skins.container.label = hack.gui.Register({
    type: 'folder',
    label: 'Skins',
    open: false
  });

  hack.modMenu.skins.container.resetSettings = hack.gui.Register({
    type: 'button',
    label: 'Unlock All',
    folder: 'Skins',
    action: function(){
      window.hack.modMenu.skins.unlockAll();
    }
  });

  hack.modMenu.misc.container.label = hack.gui.Register({
    type: 'folder',
    label: 'Misc',
    open: false
  });

  hack.modMenu.misc.container.gunPositionSelector = hack.gui.Register({
    type: 'select',
    label: 'Gun Pos :',
    object: hack.modMenu.misc,
    property: 'gunPosition',
    folder: 'Misc',
    onChange: (gunPosition) => {
      if (window.hack.myPlayerLoaded){ 
        
        if (gunPosition == 'right'){
          window.hack.myPlayer.actor.mesh._scaling.x = 1;
        }else if (gunPosition == 'left'){
          window.hack.myPlayer.actor.mesh._scaling.x = -1;
        }else if (gunPosition == 'none'){
          window.hack.myPlayer.actor.mesh._scaling.x = 0;
        }
      }
    },
    options: ['right', 'left', 'none']
  });

  hack.modMenu.misc.container.useFov = hack.gui.Register({
    type: 'checkbox',
    label: 'UseFOV : ',
    folder: 'Misc',
    object: hack.modMenu.misc,
    property: 'useFov'
  });

  hack.modMenu.misc.container.fov = hack.gui.Register({
    type: 'range',
    label: 'Your FOV:',
    min: 0,
    max: 360,
    folder: 'Misc',
    object: hack.modMenu.misc,
    property: 'fov',
  });

  hack.modMenu.render.container.label = hack.gui.Register({
    type: 'folder',
    label: 'Render',
    open: false
  });

  hack.modMenu.render.container.enabled = hack.gui.Register({
    type: 'checkbox',
    label: 'Enabled : ',
    folder: 'Render',
    object: hack.modMenu.render,
    property: 'enabled',
    onChange: (enabled)=>{
      if (!enabled){
        let scene = window.hack.myPlayer.scene;
        scene.shadowsEnabled = true;
        scene.texturesEnabled = true;
        scene.lightsEnabled = true;
        scene.particlesEnabled = true;
        scene.postProcessesEnabled = true;
        scene.renderTargetsEnabled = true;
      }
    }
  });

  hack.modMenu.render.container.shadowsEnabled = hack.gui.Register({
    type: 'checkbox',
    label: 'Shadows : ',
    folder: 'Render',
    object: hack.modMenu.render,
    property: 'shadowsEnabled'
  });

  hack.modMenu.render.container.texturesEnabled = hack.gui.Register({
    type: 'checkbox',
    label: 'Textures:',
    folder: 'Render',
    object: hack.modMenu.render,
    property: 'texturesEnabled'
  });

  hack.modMenu.render.container.lightsEnabled = hack.gui.Register({
    type: 'checkbox',
    label: 'Lights : ',
    folder: 'Render',
    object: hack.modMenu.render,
    property: 'lightsEnabled'
  });

  hack.modMenu.render.container.postProcessesEnabled = hack.gui.Register({
    type: 'checkbox',
    label: 'PostPrces:',
    folder: 'Render',
    object: hack.modMenu.render,
    property: 'postProcessesEnabled'
  });

  hack.modMenu.render.container.renderTargetsEnabled = hack.gui.Register({
    type: 'checkbox',
    label: 'RendTarg:',
    folder: 'Render',
    object: hack.modMenu.render,
    property: 'renderTargetsEnabled'
  });

  hack.modMenu.menu.container.label = hack.gui.Register({
    type: 'folder',
    label: 'Menu',
    open: false
  });

  hack.modMenu.menu.container.hideOnStart = hack.gui.Register({
    type: 'checkbox',
    label: 'Hide@Load:',
    object: hack.modMenu.menu,
    property: 'hideOnStart',
    folder: 'Menu'
  });

  hack.modMenu.menu.container.resetSettings = hack.gui.Register({
    type: 'button',
    label: 'ResetSettings',
    folder: 'Menu',
    action: function(){
      window.hack.loadSettings({});
    }
  });

  hack.modMenu.menu.container.forceSaveSettings = hack.gui.Register({
    type: 'button',
    label: 'Save Settings',
    folder: 'Menu',
    action: function(){
      window.hack.storeSettings();
    }
  });

  hack.modMenu.menu.container.currentBind = hack.gui.Register({
    type: 'display',
    label: 'FocusKey:',
    folder: 'Menu',
    object: hack.modMenu.menu,
    property: 'focusBind'
  });

  hack.modMenu.menu.container.focusBind = hack.gui.Register({
    type: 'button',
    label: 'Set Focus Key',
    folder: 'Menu',
    action: window.hack.modMenu.menu.focusBindHandler
  });

  hack.modMenu.menu.container.hideKey = hack.gui.Register({
    type: 'display',
    label: 'HideKey:',
    folder: 'Menu',
    object: hack.modMenu.menu,
    property: 'hideKey'
  });

  hack.modMenu.menu.container.setHideKey = hack.gui.Register({
    type: 'button',
    label: 'Set Hide Key',
    folder: 'Menu',
    action: window.hack.modMenu.menu.setHideKey
  });

  
  hack.modMenu.credit = hack.gui.Register({
    type: 'text',
    label: 'Credits'
  });
  
  
  window.hack.modMenu.credit.container.innerHTML = `<p style="color:orange;font-size: medium;margin-bottom: 0px;padding-left: 15px;">Created By : CrypticX</p><p style="color:orange;font-size: medium;margin-top: 0px;padding-left: 15px;">Thanks to Cryo and Sadly for their help and code!</p>`

  
  let titleTextElm = window.hack.gui.panel.panel.childNodes[0];
  titleTextElm.style.color = "rgb(0, 196, 255)";
  titleTextElm.style.fontWeight = "bold";

  
  window.hack.finishedGui();
}


window.hack.onBabylonLoad = function(){
  var esp_1 = (() => {
    const w = 0.25;
    const h = 0.65;
    return [
      new BABYLON.Vector3(-w, 0, -w),
      new BABYLON.Vector3(w, 0, -w),
      new BABYLON.Vector3(w, 0, w),
      new BABYLON.Vector3(-w, 0, w),
      new BABYLON.Vector3(-w, 0, -w),

      new BABYLON.Vector3(-w, h, -w),
      new BABYLON.Vector3(-w, 0, -w),
      new BABYLON.Vector3(w, h, -w),
      new BABYLON.Vector3(-w, h, -w),
      new BABYLON.Vector3(w, 0, -w),
      new BABYLON.Vector3(-w, h, -w),

      new BABYLON.Vector3(w, h, -w),
      new BABYLON.Vector3(w, 0, -w),
      new BABYLON.Vector3(w, h, w),
      new BABYLON.Vector3(w, h, -w),
      new BABYLON.Vector3(w, 0, w),
      new BABYLON.Vector3(w, h, -w),

      new BABYLON.Vector3(w, h, w),
      new BABYLON.Vector3(w, 0, w),
      new BABYLON.Vector3(-w, h, w),
      new BABYLON.Vector3(w, h, w),
      new BABYLON.Vector3(-w, 0, w),
      new BABYLON.Vector3(w, h, w),

      new BABYLON.Vector3(-w, h, w),
      new BABYLON.Vector3(-w, 0, w),
      new BABYLON.Vector3(-w, h, -w),
      new BABYLON.Vector3(-w, h, w),
      new BABYLON.Vector3(-w, 0, -w),
      new BABYLON.Vector3(-w, h, w),

      new BABYLON.Vector3(-w, h, -w)
    ]
  })();
  esp_2 = esp_1.map((e) => new BABYLON.Color4(1, 0.64, 0));
  window.hack.esp1 = esp_1;
  window.hack.esp2 = esp_2;
}

window.hack.modMenu.skins.onGotSkins = function(){
  window.hack.modMenu.skins.unlockAll = function(){
    for (_i in window.hack.items){
      if (_i == "shallowClone"){continue;}
      let item = window.hack.items[_i];
      extern.account.addToInventory(item);
    }
  };
  window.hack.itemsById = [];
  for (_i in window.hack.items){
    if (_i == "shallowClone"){continue;}
    let item = window.hack.items[_i];
    window.hack.itemsById[item.id] = item;
  }
}
