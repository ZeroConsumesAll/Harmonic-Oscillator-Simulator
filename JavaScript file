

var margin = {top: 20, right: 20, bottom: 30, left: 50};
var width = 1000;
var height = 400;
const padding = 30;


let xDomain = 10;
var xScale = d3.scaleLinear()
    .domain([0, xDomain])
    .range([padding, width - padding]);
var yScale = d3.scaleLinear()
    .domain([500,-500])
    .range([0, height - padding]);

let svg = d3.select('body')
    .append('svg')
        .attr('width', width + margin.left + margin.right)
        .attr('height', height + margin.top + margin.bottom);

    
var xAxis = d3.axisBottom()
    .scale(xScale)
    

svg.append('g')
    .attr('class', "x axis")
    .attr("transform", "translate(0,185)")
    .call(xAxis);

var yAxis = d3.axisLeft()
    .scale(yScale)


svg.append('g')
    .attr('class', "y axis")
    .attr("transform", "translate(30,3)")
    .call(yAxis);






var xTemp, yTemp;
let data = [];
let pointNum = 500;
let frequency = 1;
    for (let t = 0; t <= 10; t += .05) {
        yTemp = 4 * Math.sin(t)
        data.push([t, yTemp])

    }


var line_sin = d3.line()
    .x(d => xScale(d[0]))
    .y(d => yScale(d[1]))
    .curve(d3.curveMonotoneX)



svg.append('path')
    .datum(data)
    .attr('fill', 'none')
    .attr('stroke', '#263455')
    .attr('stroke-width', 2)
    .attr('d', line_sin);

   
    
function render() {
        data = [];
        var amplitude = document.getElementById('amplitude').value;
        var frequency = document.getElementById('freq').value;
        var gamma = document.getElementById('gamma').value;
        var pshift = document.getElementById('phase shift').value;

            for (let k = 0; k <= 10; k += .05) {
                yTemp = Math.exp(-gamma*k) * amplitude * Math.cos((frequency*k) + pshift);
                data.push([k, yTemp]);
            }
        
    //need to re-scale the data
        yScale = d3.scaleLinear()
            .domain([500, -500])
            .range([0, height - padding]);

        
        yAxis = d3.axisLeft()
                    .scale(yScale);
            


        //remove previously drawn y axis and x axis (get it to work)
        svg.selectAll(".y.axis").remove();

        //now add the re-scaled axes
        svg.append("g")
            .attr('class', "y axis")
            .attr("transform", "translate(30,3)")
            .call(yAxis);
            
        //remove previously drawn line
        svg.selectAll("path").remove();

        var newline = svg.selectAll(".line")
            .data(data)
            .attr("class","line");
        

        newline.enter().append("path")
                .datum(data)
                .attr("class","line")
                .attr('d', line_sin)
                .attr("fill", "none")
                .style("stroke", function(){
                    return "#"+((1<<24)*Math.random()|0).toString(16);
                  })
    
      
}


function renderCritical() {
    var data = [];
        for (let t = 0; t <= 10; t += .05) {
            amplitude = document.getElementById('amplitude').value;
            gamma = document.getElementById('gamma').value;
            yTemp =  amplitude * Math.exp(-gamma * t) + (gamma * t) * Math.exp(-gamma * t);
            data.push([t, yTemp]);
        }

        ///now add the re-scaled axes
        svg.append("g")
        .attr('class', "y axis")
        .attr("transform", "translate(30,3)")
        .call(yAxis);

        //remove previously drawn line
        svg.selectAll("path").remove();

        var newline = svg.selectAll(".line")
        .data(data)
        .attr("class","line");


        newline.enter().append("path")
            .datum(data)
            .attr("class","line")
            .attr('d', line_sin)
            .attr("fill", "none")
            .style("stroke", function(){
                return "#"+((1<<24)*Math.random()|0).toString(16);
            })
}
