<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" lang="" xml:lang="">
<head>
  <meta charset="utf-8" />
  <meta name="generator" content="pandoc" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes" />
 
  <!--[if lt IE 9]>
    <script src="//cdnjs.cloudflare.com/ajax/libs/html5shiv/3.7.3/html5shiv-printshiv.min.js"></script>
  <![endif]-->
</head>
<body>
<section id="pubg-game-prediction" class="cell markdown"
data-_cell_guid="b1076dfc-b9ad-4769-8c92-a6c4dae69d19"
data-_uuid="8f2839f25d086af736a60e9eeb907d3b93b6e0e5"
data-execution="{&quot;iopub.execute_input&quot;:&quot;2024-07-03T03:59:05.387959Z&quot;,&quot;iopub.status.busy&quot;:&quot;2024-07-03T03:59:05.387328Z&quot;,&quot;iopub.status.idle&quot;:&quot;2024-07-03T03:59:05.393797Z&quot;,&quot;shell.execute_reply&quot;:&quot;2024-07-03T03:59:05.392260Z&quot;,&quot;shell.execute_reply.started&quot;:&quot;2024-07-03T03:59:05.387914Z&quot;}">
<h1><center><font color = "green">PUBG Game
Prediction</font></center></h1>
</section>
<div class="cell markdown">
<center><img src = "https://media.giphy.com/media/XVbrX433vn6rqkexSj/giphy.gif"></center>
</div>
<div class="cell markdown">
<h2 id="about-dataset"><font color = "green">About Dataset:</font></h2>
<p>In a PUBG game, up to 100 players start in each match (matchId).
Players can be on teams (groupId) which get ranked at the end of the
game (winPlacePerc) based on how many other teams are still alive when
they are eliminated. In game, players can pick up different munitions,
revive downed-but-not-out (knocked) teammates, drive vehicles, swim,
run, shoot, and experience all of the consequences -- such as falling
too far or running themselves over and eliminating themselves.</p>
<p>You are provided with a large number of anonymized PUBG game stats,
formatted so that each row contains one player's post-game stats. The
data comes from matches of all types: solos, duos, squads, and custom;
there is no guarantee of there being 100 players per match, nor at most
4 players per group.</p>
<h3 id="link-to-dataset"><font color = "green">Link to
dataset:</font></h3>
<ul>
<li>Kaggle - <a
href="https://www.kaggle.com/datasets/ashishjangra27/pubg-games-dataset"
class="uri">https://www.kaggle.com/datasets/ashishjangra27/pubg-games-dataset</a></li>
</ul>
<h2 id="data-description"><font color = "green">Data
Description:</font></h2>
<ul>
<li><strong>DBNOs -</strong> Number of enemy players knocked.</li>
<li><strong>assists -</strong> Number of enemy players this player
damaged that were killed by teammates.</li>
<li><strong>boosts -</strong> Number of boost items used.</li>
<li><strong>damageDealt -</strong> Total damage dealt. Note: Self
inflicted damage is subtracted.</li>
<li><strong>headshotKills -</strong> Number of enemy players killed with
headshots.</li>
<li><strong>heals -</strong> Number of healing items used.</li>
<li><strong>Id -</strong> Player’s Id</li>
<li><strong>killPlace -</strong> Ranking in match of number of enemy
players killed.</li>
<li><strong>killPoints -</strong> Kills-based external ranking of
player. (Think of this as an Elo ranking where only kills matter.) If
there is a value other than -1 in rankPoints, then any 0 in killPoints
should be treated as a “None”.</li>
<li><strong>killStreaks -</strong> Max number of enemy players killed in
a short amount of time.</li>
<li><strong>kills -</strong> Number of enemy players killed.</li>
<li><strong>longestKill -</strong> Longest distance between player and
player killed at time of death. This may be misleading, as downing a
player and driving away may lead to a large longestKill stat.</li>
<li><strong>matchDuration -</strong> Duration of match in seconds.</li>
<li><strong>matchId -</strong> ID to identify match. There are no
matches that are in both the training and testing set.</li>
<li><strong>matchType -</strong> String identifying the game mode that
the data comes from. The standard modes are “solo”, “duo”, “squad”,
“solo-fpp”, “duo-fpp”, and “squad-fpp”; other modes are from events or
custom matches.</li>
<li><strong>rankPoints -</strong> Elo-like ranking of player. This
ranking is inconsistent and is being deprecated in the API’s next
version, so use with caution. Value of -1 takes place of “None”.</li>
<li><strong>revives -</strong> Number of times this player revived
teammates.</li>
<li><strong>rideDistance -</strong> Total distance traveled in vehicles
measured in meters.</li>
<li><strong>roadKills -</strong> Number of kills while in a
vehicle.</li>
<li><strong>swimDistance -</strong> Total distance traveled by swimming
measured in meters.</li>
<li><strong>teamKills -</strong> Number of times this player killed a
teammate.</li>
<li><strong>vehicleDestroys -</strong> Number of vehicles
destroyed.</li>
<li><strong>walkDistance -</strong> Total distance traveled on foot
measured in meters.-</li>
<li><strong>weaponsAcquired -</strong> Number of weapons picked up.</li>
<li><strong>winPoints -</strong> Win-based external ranking of player.
(Think of this as an Elo ranking where only winning matters.) If there
is a value other than -1 in rankPoints, then any 0 in winPoints should
be treated as a “None”.</li>
<li><strong>groupId -</strong> ID to identify a group within a match. If
the same group of players plays in different matches, they will have a
different groupId each time.</li>
<li><strong>numGroups -</strong> Number of groups we have data for in
the match.</li>
<li><strong>maxPlace -</strong> Worst placement we have data for in the
match. This may not match with numGroups, as sometimes the data skips
over placements.</li>
<li><strong>winPlacePerc -</strong> The target of prediction. This is a
percentile winning placement, where 1 corresponds to 1st place, and 0
corresponds to last place in the match. It is calculated off of
maxPlace, not numGroups, so it is possible to have missing chunks in a
match.</li>
</ul>
<h3 id="tool-and-libraries-used"><font color = "green">Tool and
Libraries Used:</font></h3>
<ul>
<li><strong>Tool:</strong>
<ul>
<li>Python 3.11.7</li>
</ul></li>
<li><strong>Standard Libraries:</strong>
<ul>
<li>warnings</li>
<li>numpy (imported as np)</li>
<li>pandas (imported as pd)</li>
</ul></li>
<li><strong>Visualization Libraries:</strong>
<ul>
<li>matplotlib.pyplot (imported as plt)</li>
<li>seaborn (imported as sns)</li>
</ul></li>
<li><strong>Machine Learning Libraries:</strong>
<ul>
<li>sklearn.preprocessing (specifically StandardScaler)</li>
<li>sklearn.model_selection (specifically train_test_split)</li>
<li>catboost (imported as cb)</li>
<li>sklearn.metrics (specifically mean_squared_error and r2_score)</li>
</ul></li>
</ul>
</div>
<section id="table-of-content" class="cell markdown">
<h3><font color = "green">Table of
Content</font><a class = "anchor" id = "content"></a></h3>
<ol>
<li><a href="#import">Importing Libraries</a></li>
<li><a href="#read">Reading the Data</a></li>
<li><a href="#wrangle">Data Wrangling</a></li>
<li><a href="#feature">Feature Engineering</a></li>
<li><a href="#cat">ML - CatBoost Model</a>
<ul>
<li><a href="#catboost">CatBoost Model</a></li>
<li><a href="#prediction">Prediction</a></li>
</ul></li>
</ol>
</section>
<section id="importing-libraries" class="cell markdown">
<h1><font color = "green">Importing
Libraries</font><a class = "anchor" id = "import"></a></h1>
</section>
<div class="cell code" data-execution_count="1">
<div class="sourceCode" id="cb1"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb1-1"><a href="#cb1-1" aria-hidden="true" tabindex="-1"></a><span class="co">## handling warnings</span></span>
<span id="cb1-2"><a href="#cb1-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb1-3"><a href="#cb1-3" aria-hidden="true" tabindex="-1"></a><span class="im">import</span> warnings</span>
<span id="cb1-4"><a href="#cb1-4" aria-hidden="true" tabindex="-1"></a>warnings.filterwarnings(<span class="st">&quot;ignore&quot;</span>)</span>
<span id="cb1-5"><a href="#cb1-5" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb1-6"><a href="#cb1-6" aria-hidden="true" tabindex="-1"></a><span class="co">##standard libraries</span></span>
<span id="cb1-7"><a href="#cb1-7" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb1-8"><a href="#cb1-8" aria-hidden="true" tabindex="-1"></a><span class="im">import</span> numpy <span class="im">as</span> np <span class="co"># linear algebra</span></span>
<span id="cb1-9"><a href="#cb1-9" aria-hidden="true" tabindex="-1"></a><span class="im">import</span> pandas <span class="im">as</span> pd <span class="co"># data processing, CSV file I/O (e.g. pd.read_csv)</span></span>
<span id="cb1-10"><a href="#cb1-10" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb1-11"><a href="#cb1-11" aria-hidden="true" tabindex="-1"></a><span class="co">## visualisation</span></span>
<span id="cb1-12"><a href="#cb1-12" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb1-13"><a href="#cb1-13" aria-hidden="true" tabindex="-1"></a><span class="im">import</span> matplotlib.pyplot <span class="im">as</span> plt</span>
<span id="cb1-14"><a href="#cb1-14" aria-hidden="true" tabindex="-1"></a><span class="op">%</span>matplotlib inline</span>
<span id="cb1-15"><a href="#cb1-15" aria-hidden="true" tabindex="-1"></a>plt.rcParams[<span class="st">&quot;figure.figsize&quot;</span>] <span class="op">=</span> (<span class="dv">11</span>,<span class="dv">5</span>)</span>
<span id="cb1-16"><a href="#cb1-16" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb1-17"><a href="#cb1-17" aria-hidden="true" tabindex="-1"></a><span class="im">import</span> seaborn <span class="im">as</span> sns</span>
<span id="cb1-18"><a href="#cb1-18" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb1-19"><a href="#cb1-19" aria-hidden="true" tabindex="-1"></a><span class="im">from</span> sklearn.preprocessing <span class="im">import</span> StandardScaler</span>
<span id="cb1-20"><a href="#cb1-20" aria-hidden="true" tabindex="-1"></a><span class="im">from</span> sklearn.model_selection <span class="im">import</span> train_test_split</span>
<span id="cb1-21"><a href="#cb1-21" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb1-22"><a href="#cb1-22" aria-hidden="true" tabindex="-1"></a><span class="co">## !pip install catboost (for jupyter/colab)</span></span>
<span id="cb1-23"><a href="#cb1-23" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb1-24"><a href="#cb1-24" aria-hidden="true" tabindex="-1"></a><span class="im">import</span> catboost <span class="im">as</span> cb</span>
<span id="cb1-25"><a href="#cb1-25" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb1-26"><a href="#cb1-26" aria-hidden="true" tabindex="-1"></a><span class="im">from</span> sklearn.metrics <span class="im">import</span> mean_squared_error</span>
<span id="cb1-27"><a href="#cb1-27" aria-hidden="true" tabindex="-1"></a><span class="im">from</span> sklearn.metrics <span class="im">import</span> r2_score</span></code></pre></div>
</div>
<div class="cell markdown">
<p><a href="#content">🔝</a></p>
</div>
<section id="reading-the-data-" class="cell markdown">
<h1><font color = "green">Reading the Data
</font><a class = "anchor" id = "read"></a></h1>
</section>
<div class="cell code" data-execution_count="2">
<div class="sourceCode" id="cb2"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb2-1"><a href="#cb2-1" aria-hidden="true" tabindex="-1"></a><span class="co">## load the data</span></span>
<span id="cb2-2"><a href="#cb2-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb2-3"><a href="#cb2-3" aria-hidden="true" tabindex="-1"></a>df <span class="op">=</span> pd.read_csv(<span class="st">&quot;pubg_game_prediction.csv&quot;</span>)</span>
<span id="cb2-4"><a href="#cb2-4" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb2-5"><a href="#cb2-5" aria-hidden="true" tabindex="-1"></a><span class="co">## glimpse of the data</span></span>
<span id="cb2-6"><a href="#cb2-6" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb2-7"><a href="#cb2-7" aria-hidden="true" tabindex="-1"></a>df.head(<span class="dv">2</span>)</span></code></pre></div>
<div class="output error" data-ename="FileNotFoundError"
data-evalue="[Errno 2] No such file or directory: &#39;pubg_game_prediction.csv&#39;">
<pre><code>---------------------------------------------------------------------------
FileNotFoundError                         Traceback (most recent call last)
Cell In[2], line 3
      1 ## load the data
----&gt; 3 df = pd.read_csv(&quot;pubg_game_prediction.csv&quot;)
      5 ## glimpse of the data
      7 df.head(2)

File ~\anaconda3\Lib\site-packages\pandas\io\parsers\readers.py:948, in read_csv(filepath_or_buffer, sep, delimiter, header, names, index_col, usecols, dtype, engine, converters, true_values, false_values, skipinitialspace, skiprows, skipfooter, nrows, na_values, keep_default_na, na_filter, verbose, skip_blank_lines, parse_dates, infer_datetime_format, keep_date_col, date_parser, date_format, dayfirst, cache_dates, iterator, chunksize, compression, thousands, decimal, lineterminator, quotechar, quoting, doublequote, escapechar, comment, encoding, encoding_errors, dialect, on_bad_lines, delim_whitespace, low_memory, memory_map, float_precision, storage_options, dtype_backend)
    935 kwds_defaults = _refine_defaults_read(
    936     dialect,
    937     delimiter,
   (...)
    944     dtype_backend=dtype_backend,
    945 )
    946 kwds.update(kwds_defaults)
--&gt; 948 return _read(filepath_or_buffer, kwds)

File ~\anaconda3\Lib\site-packages\pandas\io\parsers\readers.py:611, in _read(filepath_or_buffer, kwds)
    608 _validate_names(kwds.get(&quot;names&quot;, None))
    610 # Create the parser.
--&gt; 611 parser = TextFileReader(filepath_or_buffer, **kwds)
    613 if chunksize or iterator:
    614     return parser

File ~\anaconda3\Lib\site-packages\pandas\io\parsers\readers.py:1448, in TextFileReader.__init__(self, f, engine, **kwds)
   1445     self.options[&quot;has_index_names&quot;] = kwds[&quot;has_index_names&quot;]
   1447 self.handles: IOHandles | None = None
-&gt; 1448 self._engine = self._make_engine(f, self.engine)

File ~\anaconda3\Lib\site-packages\pandas\io\parsers\readers.py:1705, in TextFileReader._make_engine(self, f, engine)
   1703     if &quot;b&quot; not in mode:
   1704         mode += &quot;b&quot;
-&gt; 1705 self.handles = get_handle(
   1706     f,
   1707     mode,
   1708     encoding=self.options.get(&quot;encoding&quot;, None),
   1709     compression=self.options.get(&quot;compression&quot;, None),
   1710     memory_map=self.options.get(&quot;memory_map&quot;, False),
   1711     is_text=is_text,
   1712     errors=self.options.get(&quot;encoding_errors&quot;, &quot;strict&quot;),
   1713     storage_options=self.options.get(&quot;storage_options&quot;, None),
   1714 )
   1715 assert self.handles is not None
   1716 f = self.handles.handle

File ~\anaconda3\Lib\site-packages\pandas\io\common.py:863, in get_handle(path_or_buf, mode, encoding, compression, memory_map, is_text, errors, storage_options)
    858 elif isinstance(handle, str):
    859     # Check whether the filename is to be opened in binary mode.
    860     # Binary mode does not support &#39;encoding&#39; and &#39;newline&#39;.
    861     if ioargs.encoding and &quot;b&quot; not in ioargs.mode:
    862         # Encoding
--&gt; 863         handle = open(
    864             handle,
    865             ioargs.mode,
    866             encoding=ioargs.encoding,
    867             errors=errors,
    868             newline=&quot;&quot;,
    869         )
    870     else:
    871         # Binary mode
    872         handle = open(handle, ioargs.mode)

FileNotFoundError: [Errno 2] No such file or directory: &#39;pubg_game_prediction.csv&#39;
</code></pre>
</div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb4"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb4-1"><a href="#cb4-1" aria-hidden="true" tabindex="-1"></a><span class="co">## data dimension</span></span>
<span id="cb4-2"><a href="#cb4-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb4-3"><a href="#cb4-3" aria-hidden="true" tabindex="-1"></a>df.shape</span></code></pre></div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb5"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb5-1"><a href="#cb5-1" aria-hidden="true" tabindex="-1"></a><span class="co">## data information</span></span>
<span id="cb5-2"><a href="#cb5-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb5-3"><a href="#cb5-3" aria-hidden="true" tabindex="-1"></a>df.info()</span></code></pre></div>
</div>
<div class="cell markdown">
<p><a href="#content">🔝</a></p>
</div>
<section id="data-wrangling" class="cell markdown"
data-execution="{&quot;iopub.execute_input&quot;:&quot;2024-07-03T04:09:31.325863Z&quot;,&quot;iopub.status.busy&quot;:&quot;2024-07-03T04:09:31.324826Z&quot;,&quot;iopub.status.idle&quot;:&quot;2024-07-03T04:09:31.330617Z&quot;,&quot;shell.execute_reply&quot;:&quot;2024-07-03T04:09:31.329247Z&quot;,&quot;shell.execute_reply.started&quot;:&quot;2024-07-03T04:09:31.325822Z&quot;}">
<h1><font color = "green">Data
Wrangling</font><a class = "anchor" id = "wrangle"></a></h1>
</section>
<section id="check-for-the-rows-with-missing-win-prediction-value"
class="cell markdown">
<h4>Check for the rows with missing win prediction value</h4>
</section>
<div class="cell code">
<div class="sourceCode" id="cb6"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb6-1"><a href="#cb6-1" aria-hidden="true" tabindex="-1"></a><span class="co">## check row with NULL win prediction value</span></span>
<span id="cb6-2"><a href="#cb6-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb6-3"><a href="#cb6-3" aria-hidden="true" tabindex="-1"></a>df[df[<span class="st">&#39;winPlacePerc&#39;</span>].isnull()]</span></code></pre></div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb7"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb7-1"><a href="#cb7-1" aria-hidden="true" tabindex="-1"></a><span class="co">## remove the data row - 2744604</span></span>
<span id="cb7-2"><a href="#cb7-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb7-3"><a href="#cb7-3" aria-hidden="true" tabindex="-1"></a>df.drop(<span class="dv">2744604</span>, inplace <span class="op">=</span> <span class="va">True</span>)</span></code></pre></div>
</div>
<section id="understanding-players-distribution-in-a-game"
class="cell markdown">
<h4>Understanding Players distribution in a game</h4>
</section>
<div class="cell code">
<div class="sourceCode" id="cb8"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb8-1"><a href="#cb8-1" aria-hidden="true" tabindex="-1"></a><span class="co">## prepare new parameter to know how many players are in a game</span></span>
<span id="cb8-2"><a href="#cb8-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb8-3"><a href="#cb8-3" aria-hidden="true" tabindex="-1"></a>df[<span class="st">&#39;playersJoined&#39;</span>] <span class="op">=</span> df.groupby(<span class="st">&#39;matchId&#39;</span>)[<span class="st">&#39;matchId&#39;</span>].transform(<span class="st">&#39;count&#39;</span>)</span>
<span id="cb8-4"><a href="#cb8-4" aria-hidden="true" tabindex="-1"></a>df.head(<span class="dv">1</span>)</span></code></pre></div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb9"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb9-1"><a href="#cb9-1" aria-hidden="true" tabindex="-1"></a><span class="co">## visualize matches where players joined &gt;= 75</span></span>
<span id="cb9-2"><a href="#cb9-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb9-3"><a href="#cb9-3" aria-hidden="true" tabindex="-1"></a>sns.countplot(data <span class="op">=</span> df[df[<span class="st">&#39;playersJoined&#39;</span>]<span class="op">&gt;=</span><span class="dv">75</span>],x <span class="op">=</span> <span class="st">&#39;playersJoined&#39;</span>)</span>
<span id="cb9-4"><a href="#cb9-4" aria-hidden="true" tabindex="-1"></a>plt.show()</span></code></pre></div>
</div>
<section id="observation" class="cell markdown">
<h6>Observation:</h6>
<p>The data for 75 and + people in a match is huge with maximum matches
having 95-98 players</p>
</section>
<section id="analysing-the-data" class="cell markdown">
<h2>Analysing the data</h2>
</section>
<section id="kills-without-moving" class="cell markdown">
<h4>Kills Without Moving?</h4>
<h6
id="it-is-not-possible-to-kill-even-1-player-if-you-do-not-move-by-atleast-1-unit-following-are-mostly-used-practices-by-cheaters-ones-who-interfere-with-the-games-genuine-natural-processes">It
is not possible to kill even 1 player if you do not move by atleast 1
unit. Following are mostly used practices by cheaters (ones who
interfere with the game's genuine natural processes):</h6>
<ul>
<li>Aimbots</li>
<li>Wallhacks</li>
<li>Triggerbots</li>
<li>ESP (Extra Sensory Perception)</li>
<li>Silent Aim</li>
</ul>
</section>
<div class="cell code">
<div class="sourceCode" id="cb10"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb10-1"><a href="#cb10-1" aria-hidden="true" tabindex="-1"></a><span class="co">## prepare a data parameter to gather the information of the total distance travelled</span></span>
<span id="cb10-2"><a href="#cb10-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb10-3"><a href="#cb10-3" aria-hidden="true" tabindex="-1"></a>df[<span class="st">&#39;totalDistance&#39;</span>] <span class="op">=</span> df[<span class="st">&#39;rideDistance&#39;</span>] <span class="op">+</span> df[<span class="st">&#39;walkDistance&#39;</span>] <span class="op">+</span> df[<span class="st">&#39;swimDistance&#39;</span>]</span>
<span id="cb10-4"><a href="#cb10-4" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb10-5"><a href="#cb10-5" aria-hidden="true" tabindex="-1"></a><span class="co">## prepare a data parameter to check for anamoly detection that</span></span>
<span id="cb10-6"><a href="#cb10-6" aria-hidden="true" tabindex="-1"></a><span class="co">## the person has not moved but still managed to do the kills</span></span>
<span id="cb10-7"><a href="#cb10-7" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb10-8"><a href="#cb10-8" aria-hidden="true" tabindex="-1"></a>df[<span class="st">&#39;killswithoutMoving&#39;</span>] <span class="op">=</span> ((df[<span class="st">&#39;kills&#39;</span>] <span class="op">&gt;</span> <span class="dv">0</span>) <span class="op">&amp;</span> (df[<span class="st">&#39;totalDistance&#39;</span>] <span class="op">==</span> <span class="dv">0</span>))</span></code></pre></div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb11"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb11-1"><a href="#cb11-1" aria-hidden="true" tabindex="-1"></a><span class="co">## check data for people who have killed without moving</span></span>
<span id="cb11-2"><a href="#cb11-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb11-3"><a href="#cb11-3" aria-hidden="true" tabindex="-1"></a>df[df[<span class="st">&#39;killswithoutMoving&#39;</span>] <span class="op">==</span> <span class="va">True</span>].head(<span class="dv">2</span>)</span></code></pre></div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb12"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb12-1"><a href="#cb12-1" aria-hidden="true" tabindex="-1"></a><span class="co">## check total kills without moving data</span></span>
<span id="cb12-2"><a href="#cb12-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb12-3"><a href="#cb12-3" aria-hidden="true" tabindex="-1"></a>df[df[<span class="st">&#39;killswithoutMoving&#39;</span>] <span class="op">==</span> <span class="va">True</span>].shape</span></code></pre></div>
</div>
<section id="observation" class="cell markdown">
<h6>Observation:</h6>
<p>1535 instances have either used hacks or been lucky ! We cannot use
such data (which cannot be generalised) for our model. Hence, dropping
these instances.</p>
</section>
<div class="cell code">
<div class="sourceCode" id="cb13"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb13-1"><a href="#cb13-1" aria-hidden="true" tabindex="-1"></a><span class="co">## drop the instances</span></span>
<span id="cb13-2"><a href="#cb13-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb13-3"><a href="#cb13-3" aria-hidden="true" tabindex="-1"></a>df.drop(df[df[<span class="st">&#39;killswithoutMoving&#39;</span>] <span class="op">==</span> <span class="va">True</span>].index , inplace <span class="op">=</span> <span class="va">True</span>)</span></code></pre></div>
</div>
<section id="extra-ordinary-road-kills-" class="cell markdown">
<h4>Extra-ordinary Road Kills !</h4>
</section>
<div class="cell code">
<div class="sourceCode" id="cb14"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb14-1"><a href="#cb14-1" aria-hidden="true" tabindex="-1"></a><span class="co">## check data for roadkills &gt; 5</span></span>
<span id="cb14-2"><a href="#cb14-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb14-3"><a href="#cb14-3" aria-hidden="true" tabindex="-1"></a>df[df[<span class="st">&#39;roadKills&#39;</span>] <span class="op">&gt;</span> <span class="dv">5</span>].shape</span></code></pre></div>
</div>
<section id="observation" class="cell markdown">
<h6>Observation:</h6>
<p>It takes to be expert among the other players in a match to kill by
vehicles only. Hence dropping the 46 instances from data frame.</p>
</section>
<div class="cell code">
<div class="sourceCode" id="cb15"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb15-1"><a href="#cb15-1" aria-hidden="true" tabindex="-1"></a><span class="co">## drop the instance</span></span>
<span id="cb15-2"><a href="#cb15-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb15-3"><a href="#cb15-3" aria-hidden="true" tabindex="-1"></a>df.drop(df[df[<span class="st">&#39;roadKills&#39;</span>] <span class="op">&gt;</span> <span class="dv">5</span>].index, inplace <span class="op">=</span> <span class="va">True</span>)</span></code></pre></div>
</div>
<section id="so-many-kills---how-" class="cell markdown">
<h4>So many KILLS - how ???</h4>
</section>
<div class="cell code">
<div class="sourceCode" id="cb16"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb16-1"><a href="#cb16-1" aria-hidden="true" tabindex="-1"></a><span class="co">## visualize data for No. of players | Kills</span></span>
<span id="cb16-2"><a href="#cb16-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb16-3"><a href="#cb16-3" aria-hidden="true" tabindex="-1"></a>sns.countplot(data <span class="op">=</span> df, x <span class="op">=</span> df[<span class="st">&#39;kills&#39;</span>]).set_title(<span class="st">&quot;Distribution of KILLS by a player&quot;</span>)</span>
<span id="cb16-4"><a href="#cb16-4" aria-hidden="true" tabindex="-1"></a>plt.ylabel(<span class="st">&quot;Count of players&quot;</span>)</span>
<span id="cb16-5"><a href="#cb16-5" aria-hidden="true" tabindex="-1"></a>plt.xlabel(<span class="st">&quot;Number of Kills&quot;</span>)</span>
<span id="cb16-6"><a href="#cb16-6" aria-hidden="true" tabindex="-1"></a>plt.show()</span></code></pre></div>
</div>
<section id="observation" class="cell markdown">
<h6>Observation:</h6>
<p>Maximum people kills upto maximum 12 players.</p>
</section>
<div class="cell code">
<div class="sourceCode" id="cb17"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb17-1"><a href="#cb17-1" aria-hidden="true" tabindex="-1"></a><span class="co">## visualize data for No. of players | Kills &gt;= 15</span></span>
<span id="cb17-2"><a href="#cb17-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb17-3"><a href="#cb17-3" aria-hidden="true" tabindex="-1"></a>sns.countplot(data <span class="op">=</span> df[df[<span class="st">&#39;kills&#39;</span>]<span class="op">&gt;=</span><span class="dv">15</span>],x<span class="op">=</span><span class="st">&#39;kills&#39;</span>).set_title(<span class="st">&quot;Distribution of KILLS by a player&quot;</span>)</span>
<span id="cb17-4"><a href="#cb17-4" aria-hidden="true" tabindex="-1"></a>plt.ylabel(<span class="st">&quot;Count of players&quot;</span>)</span>
<span id="cb17-5"><a href="#cb17-5" aria-hidden="true" tabindex="-1"></a>plt.xlabel(<span class="st">&quot;Number of Kills&quot;</span>)</span>
<span id="cb17-6"><a href="#cb17-6" aria-hidden="true" tabindex="-1"></a>plt.show()</span></code></pre></div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb18"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb18-1"><a href="#cb18-1" aria-hidden="true" tabindex="-1"></a><span class="co">## kills &gt; 20 cannot be generalized</span></span>
<span id="cb18-2"><a href="#cb18-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb18-3"><a href="#cb18-3" aria-hidden="true" tabindex="-1"></a>df[df[<span class="st">&#39;kills&#39;</span>] <span class="op">&gt;</span> <span class="dv">20</span>].shape</span></code></pre></div>
</div>
<section id="observation" class="cell markdown">
<h6>Observation:</h6>
<p>Kills beyond 20 are rare and cannot be used a general use case.
Hence, dropping the instance.</p>
</section>
<div class="cell code">
<div class="sourceCode" id="cb19"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb19-1"><a href="#cb19-1" aria-hidden="true" tabindex="-1"></a><span class="co">## drop the instances</span></span>
<span id="cb19-2"><a href="#cb19-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb19-3"><a href="#cb19-3" aria-hidden="true" tabindex="-1"></a>df.drop(df[df[<span class="st">&#39;kills&#39;</span>] <span class="op">&gt;</span> <span class="dv">20</span>].index, inplace <span class="op">=</span> <span class="va">True</span>)</span></code></pre></div>
</div>
<section id="head-shot" class="cell markdown">
<h4>Head Shot</h4>
</section>
<div class="cell markdown">
<center><img src = "https://media.giphy.com/media/l3mZrOajz5VCZf7Hy/giphy.gif"></center>
</div>
<div class="cell code">
<div class="sourceCode" id="cb20"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb20-1"><a href="#cb20-1" aria-hidden="true" tabindex="-1"></a><span class="co">## calculate headshot rate</span></span>
<span id="cb20-2"><a href="#cb20-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb20-3"><a href="#cb20-3" aria-hidden="true" tabindex="-1"></a>df[<span class="st">&#39;headshot_rate&#39;</span>] <span class="op">=</span> df[<span class="st">&#39;headshotKills&#39;</span>]<span class="op">/</span>df[<span class="st">&#39;kills&#39;</span>]</span>
<span id="cb20-4"><a href="#cb20-4" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb20-5"><a href="#cb20-5" aria-hidden="true" tabindex="-1"></a><span class="co">## fill with 0 if there is not headshot</span></span>
<span id="cb20-6"><a href="#cb20-6" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb20-7"><a href="#cb20-7" aria-hidden="true" tabindex="-1"></a>df[<span class="st">&#39;headshot_rate&#39;</span>] <span class="op">=</span> df[<span class="st">&#39;headshot_rate&#39;</span>].fillna(<span class="dv">0</span>)</span></code></pre></div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb21"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb21-1"><a href="#cb21-1" aria-hidden="true" tabindex="-1"></a><span class="co">## plot the headshot rate distribution</span></span>
<span id="cb21-2"><a href="#cb21-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb21-3"><a href="#cb21-3" aria-hidden="true" tabindex="-1"></a>sns.distplot(df[<span class="st">&#39;headshot_rate&#39;</span>], bins <span class="op">=</span><span class="dv">10</span>).set_title(<span class="st">&quot;Distplot showing the distribution of headshot rate&quot;</span>)</span>
<span id="cb21-4"><a href="#cb21-4" aria-hidden="true" tabindex="-1"></a>plt.ylabel(<span class="st">&quot;Count of players&quot;</span>)</span>
<span id="cb21-5"><a href="#cb21-5" aria-hidden="true" tabindex="-1"></a>plt.show()</span></code></pre></div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb22"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb22-1"><a href="#cb22-1" aria-hidden="true" tabindex="-1"></a><span class="co">## find headshot rate == 100% with kills &gt; 5</span></span>
<span id="cb22-2"><a href="#cb22-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb22-3"><a href="#cb22-3" aria-hidden="true" tabindex="-1"></a>df[(df[<span class="st">&#39;headshot_rate&#39;</span>] <span class="op">==</span> <span class="dv">1</span>) <span class="op">&amp;</span> (df[<span class="st">&#39;kills&#39;</span>] <span class="op">&gt;</span> <span class="dv">5</span>)].shape</span></code></pre></div>
</div>
<section id="observation" class="cell markdown">
<h6>Observation</h6>
<p>Killing more than 5 people as headshots where all the shots in a
match are headshots is mostly not a general case. 187 instances have
such anomaly and hence, we will drop them.</p>
</section>
<div class="cell code">
<div class="sourceCode" id="cb23"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb23-1"><a href="#cb23-1" aria-hidden="true" tabindex="-1"></a><span class="co">## droping the instances</span></span>
<span id="cb23-2"><a href="#cb23-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb23-3"><a href="#cb23-3" aria-hidden="true" tabindex="-1"></a>df.drop(df[(df[<span class="st">&#39;headshot_rate&#39;</span>] <span class="op">==</span> <span class="dv">1</span>) <span class="op">&amp;</span> (df[<span class="st">&#39;kills&#39;</span>] <span class="op">&gt;</span> <span class="dv">6</span>)].index, inplace <span class="op">=</span> <span class="va">True</span>)</span></code></pre></div>
</div>
<section id="longest-shot" class="cell markdown">
<h4>Longest Shot</h4>
<h6
id="the-maximum-possible-distance-that-is-made-possible-to-snipe-from-in-pubg-is-1km-or-1000-meters-however-this-is-not-general-case-and-most-of-the-times-hackers-use-either-of-the-following-to-take-advantage-and-win-a-match">The
maximum possible distance that is made possible to snipe from in PUBG is
1km or 1000 meters. However, this is not general case and most of the
times, hackers use either of the following to take advantage and win a
match:</h6>
<ul>
<li>Sniper Aimbots</li>
<li>Bullet Speed/Trajectory Hacks</li>
<li>No Recoil/No Spread</li>
<li>Zoom Hacks</li>
</ul>
</section>
<div class="cell code">
<div class="sourceCode" id="cb24"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb24-1"><a href="#cb24-1" aria-hidden="true" tabindex="-1"></a><span class="co">## visualize Number of people | Longest Kills</span></span>
<span id="cb24-2"><a href="#cb24-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb24-3"><a href="#cb24-3" aria-hidden="true" tabindex="-1"></a>sns.distplot(df[<span class="st">&#39;longestKill&#39;</span>], bins <span class="op">=</span> <span class="dv">50</span>).set_title(<span class="st">&quot;Histogram showing the Longest Kill Distribution&quot;</span>)</span>
<span id="cb24-4"><a href="#cb24-4" aria-hidden="true" tabindex="-1"></a>plt.ylabel(<span class="st">&quot;Count of players&quot;</span>)</span>
<span id="cb24-5"><a href="#cb24-5" aria-hidden="true" tabindex="-1"></a>plt.show()</span></code></pre></div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb25"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb25-1"><a href="#cb25-1" aria-hidden="true" tabindex="-1"></a><span class="co">## calculate instances with longestkill distance &gt; 500 meters</span></span>
<span id="cb25-2"><a href="#cb25-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb25-3"><a href="#cb25-3" aria-hidden="true" tabindex="-1"></a>df[df[<span class="st">&#39;longestKill&#39;</span>]<span class="op">&gt;=</span><span class="dv">500</span>].shape</span></code></pre></div>
</div>
<section id="observation" class="cell markdown">
<h6>Observation:</h6>
<p>1747 instances have kills &gt; 500. hence, we will drop these.</p>
</section>
<div class="cell code">
<div class="sourceCode" id="cb26"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb26-1"><a href="#cb26-1" aria-hidden="true" tabindex="-1"></a><span class="co">## dropping the instances</span></span>
<span id="cb26-2"><a href="#cb26-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb26-3"><a href="#cb26-3" aria-hidden="true" tabindex="-1"></a>df.drop(df[df[<span class="st">&#39;longestKill&#39;</span>]<span class="op">&gt;=</span><span class="dv">500</span>].index, inplace <span class="op">=</span> <span class="va">True</span>)</span></code></pre></div>
</div>
<section id="weapon-change" class="cell markdown">
<h4>Weapon Change</h4>
<h6
id="in-general-people-change-upto-10-guns-in-match-avg-being-5-to-6-but-cheaters-sometimes-use-either-of-the-following-for-unlimited-recoil-guns-in-a-single-match">In
general, people change upto 10 guns in match (avg. being 5 to 6). But,
cheaters sometimes use either of the following for unlimited recoil/
guns in a single match:</h6>
<ul>
<li>Macro Scripts</li>
<li>Rapid Fire Hacks</li>
<li>Input Spoofing</li>
</ul>
</section>
<div class="cell code">
<div class="sourceCode" id="cb27"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb27-1"><a href="#cb27-1" aria-hidden="true" tabindex="-1"></a><span class="co">## visualize number of players | weapon change</span></span>
<span id="cb27-2"><a href="#cb27-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb27-3"><a href="#cb27-3" aria-hidden="true" tabindex="-1"></a>sns.distplot(df[<span class="st">&#39;weaponsAcquired&#39;</span>], bins<span class="op">=</span><span class="dv">100</span>).set_title(<span class="st">&quot;Weapons Distribution&quot;</span>)</span>
<span id="cb27-4"><a href="#cb27-4" aria-hidden="true" tabindex="-1"></a>plt.show()</span></code></pre></div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb28"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb28-1"><a href="#cb28-1" aria-hidden="true" tabindex="-1"></a><span class="co">## calculate instances with weapons acquired &gt; 15</span></span>
<span id="cb28-2"><a href="#cb28-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb28-3"><a href="#cb28-3" aria-hidden="true" tabindex="-1"></a>df[df[<span class="st">&#39;weaponsAcquired&#39;</span>]<span class="op">&gt;=</span><span class="dv">15</span>].shape</span></code></pre></div>
</div>
<section id="observation" class="cell markdown">
<h5>Observation:</h5>
<p>In 6809 instances, people have changed gun more than 15 times in a
match. Such is not a general the use case and hence, we will drop these
values.</p>
</section>
<div class="cell code">
<div class="sourceCode" id="cb29"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb29-1"><a href="#cb29-1" aria-hidden="true" tabindex="-1"></a><span class="co">## drop instance</span></span>
<span id="cb29-2"><a href="#cb29-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb29-3"><a href="#cb29-3" aria-hidden="true" tabindex="-1"></a>df.drop(df[df[<span class="st">&#39;weaponsAcquired&#39;</span>]<span class="op">&gt;=</span><span class="dv">15</span>].index, inplace <span class="op">=</span> <span class="va">True</span>)</span></code></pre></div>
</div>
<section id="exploratory-data-analysis" class="cell markdown">
<h3>Exploratory Data Analysis</h3>
</section>
<div class="cell code">
<div class="sourceCode" id="cb30"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb30-1"><a href="#cb30-1" aria-hidden="true" tabindex="-1"></a><span class="co">## final shape</span></span>
<span id="cb30-2"><a href="#cb30-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb30-3"><a href="#cb30-3" aria-hidden="true" tabindex="-1"></a>df.shape</span></code></pre></div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb31"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb31-1"><a href="#cb31-1" aria-hidden="true" tabindex="-1"></a><span class="co">## total number of null values</span></span>
<span id="cb31-2"><a href="#cb31-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb31-3"><a href="#cb31-3" aria-hidden="true" tabindex="-1"></a>df.isna().<span class="bu">sum</span>()</span></code></pre></div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb32"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb32-1"><a href="#cb32-1" aria-hidden="true" tabindex="-1"></a><span class="co">## correlation of parameter with Win Prediction</span></span>
<span id="cb32-2"><a href="#cb32-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb32-3"><a href="#cb32-3" aria-hidden="true" tabindex="-1"></a>plt.figure(figsize<span class="op">=</span>[<span class="dv">30</span>,<span class="dv">30</span>])</span>
<span id="cb32-4"><a href="#cb32-4" aria-hidden="true" tabindex="-1"></a>sns.heatmap(df.corr(numeric_only <span class="op">=</span> <span class="va">True</span>), annot <span class="op">=</span> <span class="va">True</span>)</span>
<span id="cb32-5"><a href="#cb32-5" aria-hidden="true" tabindex="-1"></a>plt.show()</span></code></pre></div>
</div>
<div class="cell markdown"
data-execution="{&quot;iopub.execute_input&quot;:&quot;2024-07-03T07:32:49.377708Z&quot;,&quot;iopub.status.busy&quot;:&quot;2024-07-03T07:32:49.376846Z&quot;,&quot;iopub.status.idle&quot;:&quot;2024-07-03T07:32:49.388886Z&quot;,&quot;shell.execute_reply&quot;:&quot;2024-07-03T07:32:49.386488Z&quot;,&quot;shell.execute_reply.started&quot;:&quot;2024-07-03T07:32:49.377638Z&quot;}">
<p><a href="#content">🔝</a></p>
</div>
<section id="feature-engineering" class="cell markdown">
<h1><font color = "green">Feature
Engineering</font><a class = "anchor" id = "feature"></a></h1>
</section>
<div class="cell code">
<div class="sourceCode" id="cb33"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb33-1"><a href="#cb33-1" aria-hidden="true" tabindex="-1"></a><span class="co">## calculate normalization factor</span></span>
<span id="cb33-2"><a href="#cb33-2" aria-hidden="true" tabindex="-1"></a><span class="co">## (100-factor)/100 = 0 for matches including 100 players</span></span>
<span id="cb33-3"><a href="#cb33-3" aria-hidden="true" tabindex="-1"></a><span class="co">## use (100-factor)/100 + 1</span></span>
<span id="cb33-4"><a href="#cb33-4" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb33-5"><a href="#cb33-5" aria-hidden="true" tabindex="-1"></a>normalising_factor <span class="op">=</span> (<span class="dv">100</span> <span class="op">-</span> df[<span class="st">&#39;playersJoined&#39;</span>]<span class="op">/</span><span class="dv">100</span>)<span class="op">+</span><span class="dv">1</span></span></code></pre></div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb34"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb34-1"><a href="#cb34-1" aria-hidden="true" tabindex="-1"></a><span class="co">## create new attributes with normalization factor</span></span>
<span id="cb34-2"><a href="#cb34-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb34-3"><a href="#cb34-3" aria-hidden="true" tabindex="-1"></a>df[<span class="st">&#39;killsNorm&#39;</span>] <span class="op">=</span> df[<span class="st">&#39;kills&#39;</span>] <span class="op">*</span> normalising_factor</span>
<span id="cb34-4"><a href="#cb34-4" aria-hidden="true" tabindex="-1"></a>df[<span class="st">&#39;damageDealtNorm&#39;</span>] <span class="op">=</span> df[<span class="st">&#39;damageDealt&#39;</span>] <span class="op">*</span> normalising_factor</span>
<span id="cb34-5"><a href="#cb34-5" aria-hidden="true" tabindex="-1"></a>df[<span class="st">&#39;maxPlaceNorm&#39;</span>] <span class="op">=</span> df[<span class="st">&#39;maxPlace&#39;</span>] <span class="op">*</span> normalising_factor</span>
<span id="cb34-6"><a href="#cb34-6" aria-hidden="true" tabindex="-1"></a>df[<span class="st">&#39;matchDurationNorm&#39;</span>] <span class="op">=</span> df[<span class="st">&#39;matchDuration&#39;</span>] <span class="op">*</span> normalising_factor</span>
<span id="cb34-7"><a href="#cb34-7" aria-hidden="true" tabindex="-1"></a>df[<span class="st">&#39;traveldistance&#39;</span>] <span class="op">=</span> df[<span class="st">&#39;walkDistance&#39;</span>]<span class="op">+</span> df[<span class="st">&#39;swimDistance&#39;</span>] <span class="op">+</span> df[<span class="st">&#39;rideDistance&#39;</span>]</span>
<span id="cb34-8"><a href="#cb34-8" aria-hidden="true" tabindex="-1"></a>df[<span class="st">&#39;healsnboosts&#39;</span>] <span class="op">=</span> df[<span class="st">&#39;heals&#39;</span>] <span class="op">+</span> df[<span class="st">&#39;boosts&#39;</span>]</span>
<span id="cb34-9"><a href="#cb34-9" aria-hidden="true" tabindex="-1"></a>df[<span class="st">&#39;assist&#39;</span>] <span class="op">=</span> df[<span class="st">&#39;assists&#39;</span>] <span class="op">+</span> df[<span class="st">&#39;revives&#39;</span>]</span></code></pre></div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb35"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb35-1"><a href="#cb35-1" aria-hidden="true" tabindex="-1"></a><span class="co">## analyze columns</span></span>
<span id="cb35-2"><a href="#cb35-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb35-3"><a href="#cb35-3" aria-hidden="true" tabindex="-1"></a>df.columns</span></code></pre></div>
</div>
<section id="removing-unwanted-columns" class="cell markdown">
<h4>Removing unwanted columns</h4>
</section>
<div class="cell code">
<div class="sourceCode" id="cb36"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb36-1"><a href="#cb36-1" aria-hidden="true" tabindex="-1"></a><span class="co">## not tampering the cleaned data, creating important dataset</span></span>
<span id="cb36-2"><a href="#cb36-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb36-3"><a href="#cb36-3" aria-hidden="true" tabindex="-1"></a>data <span class="op">=</span> df.drop(columns <span class="op">=</span> [<span class="st">&#39;Id&#39;</span>, <span class="st">&#39;groupId&#39;</span>, <span class="st">&#39;matchId&#39;</span>, <span class="st">&#39;assists&#39;</span>, <span class="st">&#39;boosts&#39;</span>, <span class="st">&#39;walkDistance&#39;</span>, <span class="st">&#39;swimDistance&#39;</span>,</span>
<span id="cb36-4"><a href="#cb36-4" aria-hidden="true" tabindex="-1"></a>                          <span class="st">&#39;rideDistance&#39;</span>, <span class="st">&#39;heals&#39;</span>, <span class="st">&#39;revives&#39;</span>, <span class="st">&#39;kills&#39;</span>, <span class="st">&#39;damageDealt&#39;</span>, <span class="st">&#39;maxPlace&#39;</span>, <span class="st">&#39;matchDuration&#39;</span>])</span></code></pre></div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb37"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb37-1"><a href="#cb37-1" aria-hidden="true" tabindex="-1"></a><span class="co">## check data dataframe</span></span>
<span id="cb37-2"><a href="#cb37-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb37-3"><a href="#cb37-3" aria-hidden="true" tabindex="-1"></a>data.head(<span class="dv">2</span>)</span></code></pre></div>
</div>
<section id="ml---catboost-model" class="cell markdown">
<h1><font color = "green">ML - Catboost
Model</font><a class = "anchor" id = "cat"></a></h1>
</section>
<section id="handling-categorical-data" class="cell markdown">
<h4>Handling categorical data</h4>
</section>
<div class="cell code">
<div class="sourceCode" id="cb38"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb38-1"><a href="#cb38-1" aria-hidden="true" tabindex="-1"></a>x <span class="op">=</span> data.drop([<span class="st">&#39;winPlacePerc&#39;</span>], axis <span class="op">=</span> <span class="dv">1</span>)</span>
<span id="cb38-2"><a href="#cb38-2" aria-hidden="true" tabindex="-1"></a>y <span class="op">=</span> data[<span class="st">&#39;winPlacePerc&#39;</span>]</span></code></pre></div>
</div>
<section id="one-hot-encoding" class="cell markdown">
<h4>One-hot Encoding</h4>
</section>
<div class="cell code">
<div class="sourceCode" id="cb39"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb39-1"><a href="#cb39-1" aria-hidden="true" tabindex="-1"></a>x <span class="op">=</span> pd.get_dummies(x, columns <span class="op">=</span> [<span class="st">&#39;matchType&#39;</span>, <span class="st">&#39;killswithoutMoving&#39;</span>])</span>
<span id="cb39-2"><a href="#cb39-2" aria-hidden="true" tabindex="-1"></a>x <span class="op">=</span> x.applymap(<span class="kw">lambda</span> x: <span class="bu">int</span>(x) <span class="cf">if</span> <span class="bu">isinstance</span>(x, <span class="bu">bool</span>) <span class="cf">else</span> x)</span>
<span id="cb39-3"><a href="#cb39-3" aria-hidden="true" tabindex="-1"></a>x.head()</span></code></pre></div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb40"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb40-1"><a href="#cb40-1" aria-hidden="true" tabindex="-1"></a>features <span class="op">=</span> x.columns</span></code></pre></div>
</div>
<section id="scaling-the-data" class="cell markdown">
<h4>Scaling the data</h4>
</section>
<div class="cell code">
<div class="sourceCode" id="cb41"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb41-1"><a href="#cb41-1" aria-hidden="true" tabindex="-1"></a><span class="co">## prevent model from giving undue preference</span></span>
<span id="cb41-2"><a href="#cb41-2" aria-hidden="true" tabindex="-1"></a><span class="co">## to instances with higher values</span></span>
<span id="cb41-3"><a href="#cb41-3" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb41-4"><a href="#cb41-4" aria-hidden="true" tabindex="-1"></a>sc <span class="op">=</span> StandardScaler()</span>
<span id="cb41-5"><a href="#cb41-5" aria-hidden="true" tabindex="-1"></a>sc.fit(x)</span>
<span id="cb41-6"><a href="#cb41-6" aria-hidden="true" tabindex="-1"></a>x <span class="op">=</span> pd.DataFrame(sc.transform(x))</span>
<span id="cb41-7"><a href="#cb41-7" aria-hidden="true" tabindex="-1"></a>x.head(<span class="dv">2</span>)</span></code></pre></div>
</div>
<section id="splitting-data" class="cell markdown">
<h4>Splitting data</h4>
</section>
<div class="cell code">
<div class="sourceCode" id="cb42"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb42-1"><a href="#cb42-1" aria-hidden="true" tabindex="-1"></a><span class="co">## train and test within the single file</span></span>
<span id="cb42-2"><a href="#cb42-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb42-3"><a href="#cb42-3" aria-hidden="true" tabindex="-1"></a>xtrain, xtest, ytrain, ytest <span class="op">=</span> train_test_split(x, y, test_size <span class="op">=</span> <span class="fl">0.3</span>, random_state <span class="op">=</span> <span class="dv">0</span>)</span>
<span id="cb42-4"><a href="#cb42-4" aria-hidden="true" tabindex="-1"></a><span class="bu">print</span>(xtrain.shape, ytrain.shape)</span>
<span id="cb42-5"><a href="#cb42-5" aria-hidden="true" tabindex="-1"></a><span class="bu">print</span>(xtest.shape, ytest.shape)</span></code></pre></div>
</div>
<section id="check" class="cell markdown">
<h5>Check:</h5>
<p><font  color = "Green"><strong>Training Parameters:</strong></font>
<strong>3105414</strong> <br> <font  color = "Green"><strong>Testing
Parameters:</strong></font> <strong>1330892</strong> <br></p>
</section>
<section id="catboost-model" class="cell markdown">
<h3><font color = "blue">CatBoost
Model</font><a class = "anchor" id = "catboost"></a></h3>
</section>
<div class="cell code">
<div class="sourceCode" id="cb43"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb43-1"><a href="#cb43-1" aria-hidden="true" tabindex="-1"></a>train_dataset <span class="op">=</span> cb.Pool(xtrain, ytrain)</span>
<span id="cb43-2"><a href="#cb43-2" aria-hidden="true" tabindex="-1"></a>test_dataset <span class="op">=</span> cb.Pool(xtest, ytest)</span></code></pre></div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb44"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb44-1"><a href="#cb44-1" aria-hidden="true" tabindex="-1"></a>model <span class="op">=</span> cb.CatBoostRegressor(loss_function<span class="op">=</span><span class="st">&#39;RMSE&#39;</span>)</span></code></pre></div>
</div>
<div class="cell code" data-scrolled="true">
<div class="sourceCode" id="cb45"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb45-1"><a href="#cb45-1" aria-hidden="true" tabindex="-1"></a><span class="co">## GRID search</span></span>
<span id="cb45-2"><a href="#cb45-2" aria-hidden="true" tabindex="-1"></a><span class="co">## run model one by one on all combinations</span></span>
<span id="cb45-3"><a href="#cb45-3" aria-hidden="true" tabindex="-1"></a><span class="co">## return the best parameter combination</span></span>
<span id="cb45-4"><a href="#cb45-4" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb45-5"><a href="#cb45-5" aria-hidden="true" tabindex="-1"></a>grid <span class="op">=</span> {<span class="st">&#39;iterations&#39;</span>: [<span class="dv">100</span>, <span class="dv">150</span>], </span>
<span id="cb45-6"><a href="#cb45-6" aria-hidden="true" tabindex="-1"></a>       <span class="st">&#39;learning_rate&#39;</span>: [<span class="fl">0.03</span>, <span class="fl">0.1</span>], </span>
<span id="cb45-7"><a href="#cb45-7" aria-hidden="true" tabindex="-1"></a>       <span class="st">&#39;depth&#39;</span>: [<span class="dv">2</span>, <span class="dv">4</span>, <span class="dv">6</span>, <span class="dv">8</span>]} <span class="co">## runs 16 combinations here</span></span>
<span id="cb45-8"><a href="#cb45-8" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb45-9"><a href="#cb45-9" aria-hidden="true" tabindex="-1"></a>model.grid_search(grid, train_dataset)</span></code></pre></div>
</div>
<section id="observations" class="cell markdown">
<h6>Observations:</h6>
<p>Our model has prepare final data after Kfold cross validation.</p>
<p><strong>Best Parameters:</strong></p>
<ul>
<li>'depth': 8</li>
<li>'learning_rate': 0.1</li>
<li>'iterations': 150}</li>
<li>'iterations': [0,....149]</li>
</ul>
</section>
<div class="cell code">
<div class="sourceCode" id="cb46"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb46-1"><a href="#cb46-1" aria-hidden="true" tabindex="-1"></a>feature_importance_df <span class="op">=</span> pd.DataFrame()</span>
<span id="cb46-2"><a href="#cb46-2" aria-hidden="true" tabindex="-1"></a>feature_importance_df[<span class="st">&#39;features&#39;</span>] <span class="op">=</span> features</span>
<span id="cb46-3"><a href="#cb46-3" aria-hidden="true" tabindex="-1"></a>feature_importance_df[<span class="st">&#39;importance&#39;</span>] <span class="op">=</span> model.feature_importances_</span>
<span id="cb46-4"><a href="#cb46-4" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb46-5"><a href="#cb46-5" aria-hidden="true" tabindex="-1"></a>feature_importance_df <span class="op">=</span> feature_importance_df.sort_values(by <span class="op">=</span> [<span class="st">&#39;importance&#39;</span>], ascending<span class="op">=</span><span class="va">False</span>)</span>
<span id="cb46-6"><a href="#cb46-6" aria-hidden="true" tabindex="-1"></a>feature_importance_df</span></code></pre></div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb47"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb47-1"><a href="#cb47-1" aria-hidden="true" tabindex="-1"></a>plt.figure(figsize<span class="op">=</span>(<span class="dv">10</span>, <span class="dv">6</span>))  <span class="co"># Adjust the figure size if needed</span></span>
<span id="cb47-2"><a href="#cb47-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb47-3"><a href="#cb47-3" aria-hidden="true" tabindex="-1"></a><span class="co"># Set the background color of the graph</span></span>
<span id="cb47-4"><a href="#cb47-4" aria-hidden="true" tabindex="-1"></a>plt.gca().set_facecolor(<span class="st">&#39;green&#39;</span>)</span>
<span id="cb47-5"><a href="#cb47-5" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb47-6"><a href="#cb47-6" aria-hidden="true" tabindex="-1"></a><span class="co"># Plot the bar chart with specified colors</span></span>
<span id="cb47-7"><a href="#cb47-7" aria-hidden="true" tabindex="-1"></a>bars <span class="op">=</span> plt.bar(feature_importance_df.features, feature_importance_df.importance, color<span class="op">=</span><span class="st">&#39;yellow&#39;</span>, edgecolor<span class="op">=</span><span class="st">&#39;white&#39;</span>)</span>
<span id="cb47-8"><a href="#cb47-8" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb47-9"><a href="#cb47-9" aria-hidden="true" tabindex="-1"></a><span class="co"># Set the labels and their colors</span></span>
<span id="cb47-10"><a href="#cb47-10" aria-hidden="true" tabindex="-1"></a>plt.ylabel(<span class="st">&quot;CatBoost Feature Importance&quot;</span>, color<span class="op">=</span><span class="st">&#39;black&#39;</span>)</span>
<span id="cb47-11"><a href="#cb47-11" aria-hidden="true" tabindex="-1"></a>plt.xticks(rotation<span class="op">=</span><span class="dv">90</span>, color<span class="op">=</span><span class="st">&#39;black&#39;</span>)</span>
<span id="cb47-12"><a href="#cb47-12" aria-hidden="true" tabindex="-1"></a>plt.yticks(color<span class="op">=</span><span class="st">&#39;black&#39;</span>)</span>
<span id="cb47-13"><a href="#cb47-13" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb47-14"><a href="#cb47-14" aria-hidden="true" tabindex="-1"></a><span class="co"># Display the plot</span></span>
<span id="cb47-15"><a href="#cb47-15" aria-hidden="true" tabindex="-1"></a>plt.show()</span></code></pre></div>
</div>
<section id="observation" class="cell markdown">
<h6>Observation:</h6>
<p>The model can be trained dropping the following parameters:</p>
<ul>
<li>matchType_normal-squad</li>
<li>vehicleDestroys</li>
<li>headshot_rate</li>
<li>matchType_normal-solo</li>
<li>matchType_normal-solo-fpp</li>
<li>matchType_crashtpp</li>
<li>matchType_normal-duo-fpp</li>
<li>matchType_normal-duo</li>
<li>matchType_flarefpp</li>
<li>headshotKills</li>
<li>killswithoutMoving_False</li>
</ul>
</section>
<section id="prediction" class="cell markdown">
<h2><font color = "Blue">Prediction</font><a class = "anchor" id = "catboost"></a></h2>
</section>
<div class="cell code">
<div class="sourceCode" id="cb48"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb48-1"><a href="#cb48-1" aria-hidden="true" tabindex="-1"></a>pred <span class="op">=</span> model.predict(xtest)</span></code></pre></div>
</div>
<div class="cell code">
<div class="sourceCode" id="cb49"><pre
class="sourceCode python"><code class="sourceCode python"><span id="cb49-1"><a href="#cb49-1" aria-hidden="true" tabindex="-1"></a><span class="co">## evaluate model</span></span>
<span id="cb49-2"><a href="#cb49-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb49-3"><a href="#cb49-3" aria-hidden="true" tabindex="-1"></a>rmse <span class="op">=</span> np.sqrt(mean_squared_error(ytest, pred)) <span class="co">## percentage of error</span></span>
<span id="cb49-4"><a href="#cb49-4" aria-hidden="true" tabindex="-1"></a>r2 <span class="op">=</span> r2_score(ytest, pred) <span class="co">## needs to be high closer to 1 (ranging from 0 to 1)</span></span>
<span id="cb49-5"><a href="#cb49-5" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb49-6"><a href="#cb49-6" aria-hidden="true" tabindex="-1"></a><span class="bu">print</span>(<span class="st">&quot;Testing performance&quot;</span>)</span>
<span id="cb49-7"><a href="#cb49-7" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb49-8"><a href="#cb49-8" aria-hidden="true" tabindex="-1"></a><span class="bu">print</span>(<span class="st">&quot;RMSE: </span><span class="sc">{:.2f}</span><span class="st">&quot;</span>.<span class="bu">format</span>(rmse))</span>
<span id="cb49-9"><a href="#cb49-9" aria-hidden="true" tabindex="-1"></a><span class="bu">print</span>(<span class="st">&quot;R2: </span><span class="sc">{:.2f}</span><span class="st">&quot;</span>.<span class="bu">format</span>(r2))</span></code></pre></div>
</div>
<section id="observation" class="cell markdown">
<h6>Observation:</h6>
<p>An 8% error with r2 Value closer to 1, which means the model accuracy
is high without being overfitting.</p>
</section>
<div class="cell markdown">
<p>Hence, <center>
<img src="https://media.giphy.com/media/KB89dMAtH79VIvxNCW/giphy.gif" style="width:80%; height:400px;">
</center></p>
</div>
<div class="cell markdown">
<p>I hope you found this analysis of PUBG game ranking prediction using
the CatBoost model both comprehensive and insightful! With an RSME of
0.08 and an R² score close to 1, the model demonstrates high accuracy in
predicting player rankings.<br><br> Your feedback is invaluable, please
share your thoughts if you enjoyed it. <br><br> Check out more such
projects <a href="https://github.com/sho-das">here</a>! 😄😅 <br><br> <a
href="#content">🔝</a></p>
</div>
</body>
</html>
