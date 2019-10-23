<!DOCTYPE html>
<html lang="en">
        <head>
                <title>Capstone</title>
                <h1 align="center">Random JQuery UI Page</h1>
                <link rel="stylesheet" 
                href="https://code.jquery.com/ui/1.12.1/themes/eggplant/jquery-ui.css">
                <script src="https://code.jquery.com/jquery-1.12.4.js"></script>
                <script src="https://code.jquery.com/ui/1.12.1/jquery-ui.js"></script>
                <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
                <!--<script src="dist/smooth-scrollbar.js"></script>-->
                <style>
                    body{background: #D7DAE5; font-family: fantasy; color:#6B7D7D;}
                    
                    #clear {
                        margin: 10px;  
                      display: flex;
                      align-items: center;
                      justify-content: center; 
                    } 
                    #modal{background:#C1D3C9; width: 100%; height: 600px; margin: 10px auto 0px; border: 1px solid #6B7D7D;}
                    #open{margin: 0 auto;}                    
                    #container{background: #8EAF9D; width: 98%; margin: 20px auto 0px;}
                    #output{background: #A6D8D4; width: 98%; height: 300px; margin: 10px; border: 1px solid #6B7D7D; overflow: auto;}
                    #input{background: #A6D8D4; width: 98%; height: 150px; margin: 10px; border: 1px solid #6B7D7D; margin-top: 20px; box-sizing: border-box;}
                    .error{color: red;}                    
                </style>
                <script>
                        $(document).ready(function(){
                          $("#open").click(function(){
                            $("#console").toggle();
                            Console.open = !Console.open;
                            if(Console.open) {
                                $("#open").text("Open Console");
                             }
                             else{
                                 $("#open").text("Close Console");
                             } 

                          });
                        });
                        </script> 

                <script type="text/javascript">
                    var Console = {
                        log : function(message){
                            $("#output").append(message + "<br/>");
                            return "";
                        },
                        profiling : false
                    };
                    $(function(){
                        $("#run").click(function() {
                            var input = $("#input"). val();
                            var input_clean = input.replace(/\n/g, "<br/>");
                            input_clean = input.replace(/\s/g, "&nbsp;");
                            var output = "";
                            var start = performance.now();
                            $("#output").append("> " + input_clean + "<br/>"); 
                            try{
                                output = String(window.eval(input));
                                output = output.replace(/\n/g, "<br/>");
                                output = output.replace(/\s/g, "&nbsp;");
                            }   
                            catch(e){
                                output = '<span class="error">' + e + '</span>';
                            }
                            var end = performance.now();
                            var perf = end - start;

                            $("#output").append(output + "<br/>"); 

                            if(Console.profiling) {
                                 $("#output").append("[Execution time: " + perf + "ms.] <br/>"); 
                            }
                            $("#output").animate({scrollTop: $("#output br").length * 20}, 1000);                     
                                                
                        });
                    });
                        $(function(){
                            $("#clear").click(function(){
                                $("#output").html("");
                                $("#input").val("");
                        });
                        $("#toggle-profiling").click(function() { 
                             Console.profiling = !Console.profiling;
                             if(Console.profiling) {
                                $("#toggle-profiling").text("Disable Profiling");
                             }
                             else{
                                 $("#toggle-profiling").text("Enable Profiling");
                             }

                        });
                        
                    });
                </script>
            </head>
            <body>
                <div id="console">Capstone
                <div id="modal">
                    <div id="container"></div>
                    <div id="output"></div>
                    <div id="my-scrollbar"></div>
                    <br/>
                    <textarea id="input"></textarea>
                    <br/>
                    <table align="center">
                        <tr>
                    <th><button id="run" class="ui-button ui-widget ui-corner-all">Run</button></th>
                    <th><button id="clear" class="ui-button ui-widget ui-corner-all">Clear</button></th>
                    <th><button id="toggle-profiling" class="ui-button ui-widget ui-corner-all">Enable Profiling</button></th>
                    </tr>
                    </table>
                    </div> 
                </div>
            </div>
            <br/>
                <table align="center"> 
                    <tr>                   
                    <th><button id ="open" class="ui-button ui-widget ui-corner-all">Close Console</button></th>
                </tr>
                </table>                  
                </div>
            </body>
</html>
