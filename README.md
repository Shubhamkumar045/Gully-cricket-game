# Gully-cricket-game
#include <iostream>
#include <vector>
#include <ctime>
using namespace std;

const int NUM_PLAYERS = 3;
const int NUM_DELIVERIES = 6;

struct Player {
    string name;
    int runsScored;
};

void simulateDelivery(Player& batsman) {
    int runs = rand() % 7; // Randomly generate runs from 0 to 6
    batsman.runsScored += runs;
    cout << "Runs scored: " << runs << endl;
}

void playInning(vector<Player>& battingTeam, vector<Player>& bowlingTeam) {
    int batsmanIndex = rand() % NUM_PLAYERS;
    int bowlerIndex = rand() % NUM_PLAYERS;

    Player& batsman = battingTeam[batsmanIndex];
    Player& bowler = bowlingTeam[bowlerIndex];

    cout << batsman.name << " is batting. " << bowler.name << " is bowling." << endl;

    for (int i = 0; i < NUM_DELIVERIES; ++i) {
        simulateDelivery(batsman);
    }
}

void displayResult(const vector<Player>& team, const string& teamName) {
    cout << "----- " << teamName << " Innings -----" << endl;
    for (const Player& player : team) {
        cout << player.name << ": " << player.runsScored << " runs" << endl;
    }
    cout << "--------------------------" << endl;
}

int main() {
    srand(time(0)); // Seed the random number generator

    vector<Player> teamA = {{"Player1", 0}, {"Player2", 0}, {"Player3", 0}};
    vector<Player> teamB = {{"Player4", 0}, {"Player5", 0}, {"Player6", 0}};

    cout << "Gully Cricket App - Two Innings Match" << endl;

    // TeamA (batting) vs. TeamB (bowling) - First Inning
    playInning(teamA, teamB);

    // TeamB (batting) vs. TeamA (bowling) - Second Inning
    playInning(teamB, teamA);

    // Display results
    displayResult(teamA, "TeamA");
    displayResult(teamB, "TeamB");

    // Compare scores to decide the winner or a tie
    int totalRunsTeamA = 0, totalRunsTeamB = 0;
    for (const Player& player : teamA) {
        totalRunsTeamA += player.runsScored;
    }
    for (const Player& player : teamB) {
        totalRunsTeamB += player.runsScored;
    }

    cout << "----- Match Result -----" << endl;
    if (totalRunsTeamA > totalRunsTeamB) {
        cout << "TeamA wins by " << (totalRunsTeamA - totalRunsTeamB) << " runs." << endl;
    } else if (totalRunsTeamA < totalRunsTeamB) {
        cout << "TeamB wins by " << (totalRunsTeamB - totalRunsTeamA) << " runs." << endl;
    } else {
        cout << "It's a tie!" << endl;
    }
