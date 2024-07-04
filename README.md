# Kotlin-Is-Fun

import androidx.compose.desktop.ui.tooling.preview.Preview
import androidx.compose.foundation.background
import androidx.compose.foundation.layout.Box
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.offset
import androidx.compose.material.Button
import androidx.compose.material.MaterialTheme
import androidx.compose.material.Text
import androidx.compose.runtime.Composable
import androidx.compose.runtime.getValue
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember
import androidx.compose.runtime.setValue
import androidx.compose.ui.Alignment
import androidx.compose.ui.ExperimentalComposeUiApi
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.input.pointer.PointerEventType
import androidx.compose.ui.input.pointer.onPointerEvent
import androidx.compose.ui.modifier.modifierLocalConsumer
import androidx.compose.ui.unit.DpSize
import androidx.compose.ui.unit.IntOffset
import androidx.compose.ui.unit.dp
import androidx.compose.ui.window.Window
import androidx.compose.ui.window.application
import androidx.compose.ui.window.rememberWindowState
import kotlin.random.Random
import kotlin.random.nextInt

private const val WIDTH = 1280
private const val HEIGHT = 720

@OptIn(ExperimentalComposeUiApi::class)
@Composable
@Preview
fun App() {
    var answerYes by remember { mutableStateOf(false) }
    var buttonPos by remember {mutableStateOf(IntOffset(x=50, y=0) )}
    MaterialTheme {
        Box(modifier = Modifier.fillMaxSize().background(Color(0.95f, 0.95f, 0.95f)))
        {
            Text(
                text = "Should we hire João Bernardo?",
                modifier = Modifier.align(Alignment.Center).offset(y = (-50).dp)
            )

            Button(onClick = { answerYes =!answerYes}, modifier = Modifier
                .align(Alignment.Center)
                .offset(x= (-50).dp)
                )
            { Text(text = "Yes!") }

            Button(onClick = { }, modifier = Modifier
                .align(Alignment.Center)
                .offset{buttonPos}
                .onPointerEvent(PointerEventType.Enter) {

                    val xo = (WIDTH / 2 )
                    val yo = (HEIGHT / 2 )

                    val x = Random.nextInt (-xo..xo)
                    val y = Random.nextInt (-yo..yo)
                    buttonPos= IntOffset(x=x, y=y)
                }
            ){ Text(text = "No") }
            if (answerYes)
            Text ( text= "Great News!", modifier=Modifier.align(Alignment.Center). offset(y=(50).dp))


        }
    }
}

fun main() = application {
        Window(
            onCloseRequest = ::exitApplication,
            resizable = false,
            state = rememberWindowState(size = DpSize(width = WIDTH.dp, HEIGHT.dp))
        ) {
            App()
        }
    }
