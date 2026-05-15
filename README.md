# League of Legends E-Sports Match Prediction

Course: STAT 440, Fall 2025 
Instructor: Lloyd Elliott 
Team Members: Stuart Siu, Elysa Lin, Geoffrey Ze-Yu Gao, Varinder Singh, Min Kaung Khant 

## Access Note: 
To comply with academic integrity policies, the raw datasets and source code for this project have been compressed into a password-protected .rar file within this repository. The methodology and some EDA visuals remain public. 

## Project Overview
This project focuses on predicting the outcomes of professional League of Legends (LoL) games played in 2023, utilizing historical match data spanning from 2018 to 2022. The objective was to accurately forecast three specific targets for each test game: the winning team, the individual kill counts for all 10 players, and the total game length.  

## Methodology & Predictive Pipeline
Our team developed a multi-stage predictive pipeline, utilizing Generalized Linear Mixed Models (GLMMs) to capture the hierarchical relationships between players, champions, positions, and leagues.  

### Win Probability (Logistic GLMM): 
We first generated a per-player meta-feature that estimated the probability of winning. We fit a mixed-effects logistic model on the training set with random intercepts for player ID, player-champion, player-position, champion-position, and league ID combinations.  

<img width="50%" alt="leagueodds_resim" src="https://github.com/user-attachments/assets/0afebf7e-02ab-41e2-9c76-958ab02b70b9" />

### Player Kills (ZINB GLMM): 
To address heavy zero-inflation (particularly for support roles), we utilized a Zero-Inflated Negative Binomial GLMM to predict individual kills. This model leveraged the predicted win probabilities from the first stage as a key predictor.  

<img width="50%" alt="player_kills" src="https://github.com/user-attachments/assets/df408775-3eed-4857-9c5a-b598f13e1005" />

### Game Length (Gamma GLMM): 
We implemented a Gamma GLMM to predict the length of the match, utilizing team win-probability differences and total kills as input features.  

Experimental Elo Ratings: We also experimented with implementing an Elo-style rating system to dynamically track player and team skill over time, which provided a time-varying performance indicator.  

<img width="50%" alt="Rplot" src="https://github.com/user-attachments/assets/b726f06d-b544-41ae-8111-f6a6e3885e10" />

## Tools & Technologies
- Data Processing & EDA: We initially used Excel pivot tables for rapid structural visualization, followed by Python to generate violin plots of post-game statistics.  
- Modeling: The core predictive models were written in R.  
- Key R Libraries: glmmTMB, lme4, dplyr, tidyr, readr, pROC, and ggplot2.  
- Collaboration: Version control was managed via a branch-based workflow on GitHub, supplemented by Discord for daily communication. 
