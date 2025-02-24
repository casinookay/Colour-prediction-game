# Colour-prediction-game
import React, { useState, useEffect } from "react";

const ColorPredictionGame = () => { const [balance, setBalance] = useState(1000); const [betAmount, setBetAmount] = useState(100); const [selectedColor, setSelectedColor] = useState(null); const [winningColor, setWinningColor] = useState(null); const [isBetPlaced, setIsBetPlaced] = useState(false); const [manualResult, setManualResult] = useState(null); const [isManualMode, setIsManualMode] = useState(false);

const colors = ["Red", "Green", "Blue"];

const placeBet = (color) => { if (betAmount > balance) { alert("Insufficient balance!"); return; } setSelectedColor(color); setIsBetPlaced(true); };

const generateResult = () => { if (isManualMode && manualResult) { setWinningColor(manualResult); } else { const randomIndex = Math.floor(Math.random() * colors.length); setWinningColor(colors[randomIndex]); } };

useEffect(() => { if (isBetPlaced) { setTimeout(() => { generateResult(); if (winningColor === selectedColor) { setBalance(balance + betAmount); alert("You won!"); } else { setBalance(balance - betAmount); alert("You lost!"); } setIsBetPlaced(false); }, 2000); } }, [isBetPlaced]);

return ( <div style={{ textAlign: "center", padding: "20px" }}> <h1>Color Prediction Game</h1> <h2>Balance: ₹{balance}</h2> <input type="number" value={betAmount} onChange={(e) => setBetAmount(Number(e.target.value))} disabled={isBetPlaced} /> <div style={{ marginTop: "20px" }}> {colors.map((color) => ( <button key={color} style={{ margin: "10px", padding: "10px 20px" }} onClick={() => placeBet(color)} disabled={isBetPlaced} > {color} </button> ))} </div> {winningColor && <h3>Winning Color: {winningColor}</h3>} <div style={{ marginTop: "20px" }}> <button onClick={() => setIsManualMode(!isManualMode)}> {isManualMode ? "Switch to Auto Mode" : "Switch to Manual Mode"} </button> {isManualMode && ( <div> <h3>Set Manual Result:</h3> {colors.map((color) => ( <button key={color} style={{ margin: "10px", padding: "10px 20px" }} onClick={() => setManualResult(color)} > {color} </button> ))} </div> )} </div> </div> ); };

export default ColorPredictionGame;

