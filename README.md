package br.com.luizg.alcoolOuGasolina

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.activity.enableEdgeToEdge
import androidx.compose.foundation.background
import androidx.compose.foundation.layout.Arrangement
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Spacer
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.padding
import androidx.compose.foundation.layout.size
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.Scaffold
import androidx.compose.material3.Surface
import androidx.compose.material3.Text
import androidx.compose.material3.TextField
import androidx.compose.runtime.Composable
import androidx.compose.runtime.getValue
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember
import androidx.compose.runtime.setValue
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.text.TextStyle
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import br.com.luizg.alcoolOuGasolina.ui.theme.AlcoolOuGasolinaTheme

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContent {
            AlcoolOuGasolinaTheme {

                Surface(
                    modifier = Modifier.fillMaxSize(),
                    color = MaterialTheme.colorScheme.background
                ) {
                    App()
                }
            }
        }
    }
}

@Composable
fun App() {

    var valorGasolina by remember {
        mutableStateOf(value = "")
    }
    var valorAlcool by remember {
        mutableStateOf(value = "")
    }

    Column(
        Modifier
            .background(color = Color(0xFF02A7F3))
            .fillMaxSize(),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Column(
            verticalArrangement = Arrangement.spacedBy(16.dp),
            horizontalAlignment = Alignment.CenterHorizontally
        ) {
            Text(
                text = "Álcool ou Gasolina?",
                style = TextStyle(
                    color = Color.White,
                    fontSize = 32.sp,
                    FontWeight.Bold
                )
            )
            if (valorAlcool.isNotBlank() && valorGasolina.isNotBlank()) {
                val ehGasolina = valorAlcool.toDouble() / valorGasolina.toDouble() > 0.7
                val alcoolOuGasolina = if (ehGasolina) {
                    "Gasolina"
                } else {
                    "Álcool"
                }
                val cor = if (ehGasolina) {
                    Color.Red
                } else {
                    Color.Green
                }
                Text(
                    text = alcoolOuGasolina,
                    style = TextStyle(
                        color = cor,
                        fontSize = 40.sp,
                        FontWeight.Bold
                    )
                )
            }

            TextField(
                value = valorGasolina,
                onValueChange = {

                    if (it.all { char -> char.isDigit() || char == '.' }) {
                        valorGasolina = it
                    }
                },
                label = {
                    Text(text = "Gasolina")
                }
            )
            TextField(
                value = valorAlcool,
                onValueChange = {

                    if (it.all { char -> char.isDigit() || char == '.' }) {
                        valorAlcool = it
                    }
                },
                label = {
                    Text(text = "Álcool")
                }
            )
        }
    }
}

@Preview
@Composable
fun AppPreview() {
    AlcoolOuGasolinaTheme {
        App()
    }
}
